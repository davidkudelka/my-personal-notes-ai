  * tags: #fundamentals #testing #javascript #javascript #mocking
  * Author: [[Kent C. Dodds]]
  * Notes:
    * You can run into the issue that some modules are just too hard to test, so the only thing possible is to mock the module
    * ## Monkey Patching
      * First way how to mock is monkey patching
      * ```javascript
const utils = require('./utils')

function thumbWar(player1, player2) {
  const numberToWin = 2
  let player1Wins = 0
  let player2Wins = 0
  while (player1Wins < numberToWin && player2Wins < numberToWin) {
    const winner = utils.getWinner(player1, player2)
    if (winner === player1) {
      player1Wins++
    } else if (winner === player2) {
      player2Wins++
    }
  }
  return player1Wins > player2Wins ? player1 : player2
}

module.exports = thumbWar```
      * We will for our test purposes mock out utils.getWinner function
      * here is the test
      * ```javascript
const assert = require('assert')
const thumbWar = require('../thumb-war')
const utils = require('../utils')

const originalGetWinner = utils.getWinner
utils.getWinner = (p1, p2) => p1

const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
assert.strictEqual(winner, 'Kent C. Dodds')

// cleanup
utils.getWinner = originalGetWinner```
      * Notice that it is very important to clean up after yourself, after the test **utils.getWinner = originalGetWinner**, we are setting it back to normal
    * ## Mock Function
      * ```javascript
test('returns winner', () => {
  const originalGetWinner = utils.getWinner
  utils.getWinner = jest.fn((p1, p2) => p1)

  const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
  expect(winner).toBe('Kent C. Dodds')
  expect(utils.getWinner.mock.calls).toEqual([
    ['Kent C. Dodds', 'Ken Wheeler'],
    ['Kent C. Dodds', 'Ken Wheeler']
  ])
  // could also do these assertions:
  expect(utils.getWinner).toHaveBeenCalledTimes(2)
  expect(utils.getWinner).toHaveBeenNthCalledWith(
    1,
    'Kent C. Dodds',
    'Ken Wheeler'
  )
  expect(utils.getWinner).toHaveBeenNthCalledWith(
    2,
    'Kent C. Dodds',
    'Ken Wheeler'
  )

  // cleanup
  utils.getWinner = originalGetWinner
})```
      * If we are going to wrap our mocked function in the jest function, we have much better control over the arguments with which the function is called
      * We can see that we have access to the properties as, how many the function was called and with which arguments
      * There is custom implementation of such function
        * ```javascript
const assert = require('assert')
const thumbWar = require('../thumb-war')
const utils = require('../utils')

function fn(impl) {
  const mockFn = (...args) => {
    mockFn.mock.calls.push(args)
    return impl(...args)
  }
  mockFn.mock = {calls: []}
  return mockFn
}

const originalGetWinner = utils.getWinner
utils.getWinner = fn((p1, p2) => p1)

const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
assert.strictEqual(winner, 'Kent C. Dodds')
assert.deepStrictEqual(utils.getWinner.mock.calls, [
  ['Kent C. Dodds', 'Ken Wheeler'],
  ['Kent C. Dodds', 'Ken Wheeler']
])

// cleanup
utils.getWinner = originalGetWinner```
    * ## Spy On Function
      * If we want to automate a little bit restoring the mocked values on a function we can use jest.spyOn
        * ```javascript
const thumbWar = require('../thumb-war')
const utils = require('../utils')

test('returns winner', () => {
  jest.spyOn(utils, 'getWinner')
  utils.getWinner.mockImplementation((p1, p2) => p1)

  const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
  expect(winner).toBe('Kent C. Dodds')
  expect(utils.getWinner.mock.calls).toEqual([
    ['Kent C. Dodds', 'Ken Wheeler'],
    ['Kent C. Dodds', 'Ken Wheeler']
  ])

  // cleanup
  utils.getWinner.mockRestore()
})```
        * As you can see we are using jest.spyOn on the whole utils module, then assigning mockImplementation and then restoring
      * Here is custom implementation so you can understand it better
        * ```javascript
const assert = require('assert')
const thumbWar = require('../thumb-war')
const utils = require('../utils')

function fn(impl = () => {}) {
  const mockFn = (...args) => {
    mockFn.mock.calls.push(args)
    return impl(...args)
  }
  mockFn.mock = {calls: []}
  mockFn.mockImplementation = newImpl => (impl = newImpl)
  return mockFn
}

function spyOn(obj, prop) {
  const originalValue = obj[prop]
  obj[prop] = fn()
  obj[prop].mockRestore = () => (obj[prop] = originalValue)
}

spyOn(utils, 'getWinner')
utils.getWinner.mockImplementation((p1, p2) => p1)

const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
assert.strictEqual(winner, 'Kent C. Dodds')
assert.deepStrictEqual(utils.getWinner.mock.calls, [
  ['Kent C. Dodds', 'Ken Wheeler'],
  ['Kent C. Dodds', 'Ken Wheeler']
])

// cleanup
utils.getWinner.mockRestore()```
        * Steps
          * First we are creating new property on utils module called mockRestore and saving there originalValue
          * We have created as well mock function on the original property, for now with empty function
          * We can call mockImplementation on the property to assign new mocked function
          * Everything is restored by mockRestore()
    * ## Mock Module
      * Sometimes we just need to mock the whole module, instead of monkey patching one function
        * ```javascript
const thumbWar = require('../thumb-war')
const utilsMock = require('../utils')

jest.mock('../utils', () => {
  return {
    getWinner: jest.fn((p1, p2) => p1)
  }
})

test('returns winner', () => {
  const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
  expect(winner).toBe('Kent C. Dodds')
  expect(utilsMock.getWinner.mock.calls).toEqual([
    ['Kent C. Dodds', 'Ken Wheeler'],
    ['Kent C. Dodds', 'Ken Wheeler']
  ])

  // cleanup
  utilsMock.getWinner.mockReset()
})```
        * It mocks the whole module, we just provide function to jest that replaces the utils module
      * Custom solution
        * ```javascript
function fn(impl = () => {}) {
  const mockFn = (...args) => {
    mockFn.mock.calls.push(args)
    return impl(...args)
  }
  mockFn.mock = {calls: []}
  return mockFn
}

const utilsPath = require.resolve('../utils')
require.cache[utilsPath] = {
  id: utilsPath,
  filename: utilsPath,
  loaded: true,
  exports: {
    getWinner: fn((p1, p2) => p1)
  }
}

const assert = require('assert')
const thumbWar = require('../thumb-war')
const utils = require('../utils')

const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
assert.strictEqual(winner, 'Kent C. Dodds')
assert.deepStrictEqual(utils.getWinner.mock.calls, [
  ['Kent C. Dodds', 'Ken Wheeler'],
  ['Kent C. Dodds', 'Ken Wheeler']
])

// cleanup
delete require.cache[utilsPath]```
        * We take control of cache  and we set exports of this cache to the new exports which contains our getWinner mock function
      * ### Making global mock
        * It can happen that we want to make global mock, if we are mocking one module on one place, we probably want to mock this module on multiple places
          * ![[Roam/david_kudelka_notes/Attachments/imgs/app/david_kudelka_notes/BL3yuCFMr6.png]]
          * we create utils.js file inside *mocks* folder
          * ```javascript
const thumbWar = require('../thumb-war')
const utilsMock = require('../utils')

jest.mock('../utils')

test('returns winner', () => {
  const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
  expect(winner).toBe('Kent C. Dodds')
  expect(utilsMock.getWinner.mock.calls).toEqual([
    ['Kent C. Dodds', 'Ken Wheeler'],
    ['Kent C. Dodds', 'Ken Wheeler']
  ])

  // cleanup
  utilsMock.getWinner.mockReset()
})```
          * This way it takes the default settings from mock folder
        * Custom solution
          * ```javascript
require('../*no-framework-mocks*/utils') // prime the cache
const utilsPath = require.resolve('../utils')
const mockUtilsPath = require.resolve('../*no-framework-mocks*/utils')
require.cache[utilsPath] = require.cache[mockUtilsPath]

const assert = require('assert')
const thumbWar = require('../thumb-war')
const utils = require('../utils')

const winner = thumbWar('Kent C. Dodds', 'Ken Wheeler')
assert.strictEqual(winner, 'Kent C. Dodds')
assert.deepStrictEqual(utils.getWinner.mock.calls, [
  ['Kent C. Dodds', 'Ken Wheeler'],
  ['Kent C. Dodds', 'Ken Wheeler']
])

// cleanup
delete require.cache[utilsPath]```
          * It works the same way as if we would set it manually, but there as well require.resolve from no framework folder that replaces this require.cache of the module