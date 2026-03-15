  * tags: #fundamentals #testing #javascript #javascript
  * Author: [[Kent C. Dodds]]
  * Notes:
    * # Testing Pure Functions
      * We have simple pure function on our backend, and we want to write some unit tests for this **pure function**
        * ```javascript
function isPasswordAllowed(password) {
  return (
    password.length > 6 &&
    // non-alphanumeric
    /\W/.test(password) &&
    // digit
    /\d/.test(password) &&
    // capital letter
    /[A-Z]/.test(password) &&
    // lowercase letter
    /[a-z]/.test(password)
  )
}```
        * Some simple unit tests would look like this
        * ```javascript
test(`allows abcAJADs`, () => {
   expect(isPasswordAllowed('abcAJADs')).toBe(true)
})```
      * This approach seems fine, unless we got into the situation, where we want to add much more test cases and things starts to get messy
      * Fortunately we can do very simple automation in our tests
        * ```javascript
describe('isPasswordAllowed only allows some passwords', () => {
  const allowedPasswords = ['!aBc123']
  const disallowedPasswords = [
    'a2c!',
    '123456!',
    'ABCdef!',
    'abc123!',
    'ABC123!',
    'ABCdef123',
  ]

  allowedPasswords.forEach(password => {
    test(`allows ${password}`, () => {
      expect(isPasswordAllowed(password)).toBe(true)
    })
  })

  disallowedPasswords.forEach(password => {
    test(`disallows ${password}`, () => {
      expect(isPasswordAllowed(password)).toBe(false)
    })
  })
})```
      * We can take this automation to another level, with jest-in-case library that helps us handle test cases
        * ```javascript
import cases from 'jest-in-case'
import {isPasswordAllowed} from '../auth'

cases(
  'isPasswordAllowed: valid passwords',
  ({password}) => {
    expect(isPasswordAllowed(password)).toBe(true)
  },
  {
    'valid password': {
      password: '!aBc123',
    },
  },
)

cases(
  'isPasswordAllowed: invalid passwords',
  ({password}) => {
    expect(isPasswordAllowed(password)).toBe(false)
  },
  {
    'too short': {
      password: 'a2c!',
    },
    'no letters': {
      password: '123456!',
    },
    'no numbers': {
      password: 'ABCdef!',
    },
    'no uppercase letters': {
      password: 'abc123!',
    },
    'no lowercase letters': {
      password: 'ABC123!',
    },
    'no non-alphanumeric characters': {
      password: 'ABCdef123',
    },
  },
)```
      * We have almost perfect tests, the only thing that is missing in our tests is when one of the tests cases fail, we do not immediately see what password string it actually was, let's improve it with **custom** casify function
        * ```javascript
import cases from 'jest-in-case'
import {isPasswordAllowed} from '../auth'

function casify(obj) {
  return Object.entries(obj).map(([name, password]) => ({
    name: `${password} - ${name}`,
    password,
  }))
}

cases(
  'isPasswordAllowed: valid passwords',
  ({password}) => {
    expect(isPasswordAllowed(password)).toBe(true)
  },
  casify({'valid password': '!aBc123'}),
)

cases(
  'isPasswordAllowed: invalid passwords',
  ({password}) => {
    expect(isPasswordAllowed(password)).toBe(false)
  },
  casify({
    'too short': 'a2c!',
    'no letters': '123456!',
    'no numbers': 'ABCdef!',
    'no uppercase letters': 'abc123!',
    'no lowercase letters': 'ABC123!',
    'no non-alphanumeric characters': 'ABCdef123',
  }),
)```
        * Such solution is extremely important if we want to keep our tests as short as possible with keeping the important logic together and concise
    * # Testing Node Middleware
      * We are going to test [[Node.js - Express Middleware]]
      * We have this error-handler middlware in our express
        * ```javascript
import {UnauthorizedError} from 'express-jwt'

function errorMiddleware(error, req, res, next) {
  if (res.headersSent) {
    next(error)
  } else if (error instanceof UnauthorizedError) {
    res.status(401)
    res.json({code: error.code, message: error.message})
  } else {
    res.status(500)
    res.json({
      message: error.message,
      // we only add a `stack` property in non-production environments
      ...(process.env.NODE_ENV === 'production' ? null : {stack: error.stack}),
    })
  }
}

export default errorMiddleware```
      * This is our initial version of test for this middleware
      * Something before we start is to realise what functions do you need to mock from the arguments of the function, so you can keep better track of what is happening with them inside the tests
        * ```javascript
import {UnauthorizedError} from 'express-jwt'
import errorMiddleware from '../error-middleware'

test('responds with 401 for express-jwt UnauthorizedError', () => {
  const code = 'some_error_code'
  const message = 'Some message'

  const error = new UnauthorizedError(code, {
    message,
  })
  const req = {}
  const res = {json: jest.fn(() => res), status: jest.fn(() => res)}
  const next = jest.fn()

  errorMiddleware(error, req, res, next)

  expect(next).not.toHaveBeenCalled()
  expect(res.status).toHaveBeenCalledWith(401)
  expect(res.status).toHaveBeenCalledTimes(1)
  expect(res.json).toHaveBeenCalledWith({
    code: error.code,
    message: error.message,
  })
  expect(res.json).toHaveBeenCalledTimes(1)
})```
        * In this case we are mocking res.json, res.status and next function
        * those mock function as well returns back the res object because normally we can chain those function on top of each other
        * Very important thing to test here not only that res.json and res.status were called with correct arguments but as well **how many times** we called those functions