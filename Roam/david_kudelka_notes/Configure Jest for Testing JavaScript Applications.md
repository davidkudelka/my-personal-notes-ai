  * tags: #fundamentals #testing #javascript #javascript #jest
  * Author: [[Kent C. Dodds]]
  * Notes:
    * We will be using jest
    * `npm install --save-dev jest`
    * We can then add just simple script to the package.json
      * `"test": "jest",`
    * Jest automatically detects any file in the project folder which are in either
      * folder with name `*tests*`
      * named **.test.js
    * You can access NODE_ENV while running jest tests and this NODE_ENV = 'test', based on this you can provide different settings for different use cases
    * Jest simulates browser environment in Node, you can access window object
    * `jest.config.js`
      * ```javascript
module.exports = {
  testEnvironment: 'jest-environment-jsdom',
  moduleNameMapper: {
    '\\.css$': require.resolve('./test/style-mock.js'),
  },
}```
      * By testEnvironment we are setting basic environment where our tests run, it can be either 'jest-environment-jsdom' or 'jest-environment-node'
      * moduleNameMapper here works as webpack, we need to somehow resolve .css file, and by this we can just export in /test/style-mock.js file empty object, at this point we don't need any css actually, because we are testing functionality not the css
    * ### CSS files support
      * If you want to support name of your CSS classes for testing, because you want to check what class was applied to your component
      * `npm install --save dev identity-obj-proxy`
      * ```javascript
module.exports = {
  testEnvironment: 'jest-environment-jsdom',
  moduleNameMapper: {
    '\\.module\\.css$': 'identity-obj-proxy',
    '\\.css$': require.resolve('./test/style-mock.js'),
  }
}```
    * ### Snapshots
      * You can expect snapshot of some tests by
      * `expect(flyingHeros).toMatchSnapshot()`
      * This basically saves the result of the test and save is to its own file
      * There are 2 types of snapshots
        * `expect(flyingHeros).toMatchSnapshot()`
        * `expect(container).toMatchInlineSnapshot()`
          * This has advantage in keeping the result of the snapshot in same folder
    * ### Snapshots with emotion (CSS)
      * If you are using emotion for css, you can install `npm install --save-dev @emotion/jest`
        * ```javascript
module.exports = {
  testEnvironment: 'jest-environment-jsdom',
  moduleNameMapper: {
    '\\.module\\.css$': 'identity-obj-proxy',
    '\\.css$': require.resolve('./test/style-mock.js'),
  },
  snapshotSerializers: ['@emotion/jest/serializer'],
}```
      * To see actual css in the snapshot instead of just generated class
    * ### Custom Module Resolution
      * If you set in your webpack custom module resolution, meaning importing
      * you can adjust you jest config to behave the same way
        * ```javascript
const path = require('path')

module.exports = {
  testEnvironment: 'jest-environment-jsdom',
  moduleDirectories: ['node_modules', path.join(__dirname, 'src'), 'shared'],
  moduleNameMapper: {
    '\\.module\\.css$': 'identity-obj-proxy',
    '\\.css$': require.resolve('./test/style-mock.js'),
  },
  snapshotSerializers: ['jest-emotion'],
}```
          * Added line with moduleDirectories
    * ### setupFilesAfterEnv
      * If you want to setup some import for jest tests before you run them you can use config
        * ```javascript
const path = require('path')

module.exports = {
  testEnvironment: 'jest-environment-jsdom',
  moduleDirectories: ['node_modules', path.join(__dirname, 'src'), 'shared'],
  moduleNameMapper: {
    '\\.module\\.css$': 'identity-obj-proxy',
    '\\.css$': require.resolve('./test/style-mock.js'),
  },
  setupFilesAfterEnv: ['@testing-library/jest-dom/extend-expect'],
  snapshotSerializers: ['jest-emotion'],
}```
        * Look at the setupFilesAfterEnv
        * What basically avoid to import in all files we want to use this package this code
        * `import '@testing-library/jest-dom/extend-expect'`
    * ### setup Test Utilities with Jest moduleDirectories
      * If you want to create custom render method for your tests, that for example wrap your theme around all components, so you can properly test everything with theme provider
      * You can create this file in your test folder
        * ```javascript
import React from 'react'
import PropTypes from 'prop-types'
import {render as rtlRender} from '@testing-library/react'
import {render} from '@testing-library/react'
import {ThemeProvider} from 'emotion-theming'
import {dark} from '../src/themes'

function render(ui, {theme = themes.dark, ...options}) {
  function Wrapper({children}) {
    return <ThemeProvider theme={theme}>{children}</ThemeProvider>
}
Wrapper.propTypes = {
  children: PropTypes.node,
}
  return rtlRender(ui, {wrapper: Wrapper, ...options}}
}

export * from '@testing-librasry/react'
export {render}```
      * Add this to your moduleDirectories jest config
        * ```javascript
moduleDirectories: [
  'node_modules',
  path.join(__dirname, 'src'),
  'shared',
  path.join(__dirname, 'test'),
],```
      * This fix your tests, but you still need to fix your .eslint
        * `npm install --save-dev eslint-import-resolver-jest`
      * Add special overrides to your .eslint
        * ```javascript
  overrides: [
    {
      files: ['**/src/**'],
      settings: {'import/resolver': 'webpack'},
    },
    {
      files: ['**/*test*/**'],
      settings: {
        'import/resolver': {
          jest: {
            jestConfigFile: path.join(__dirname, './jest.config)
        },
    }},
  ],```
      * Then just adding in your tsconfig or jsconfig.json everything to the path and include
        * ```javascript
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "*": ["src/*", "src/shared/*", "test/*"]
    }
  },
  "include": ["src", "test/*"]
}```
        * Pay attention to the test/*
