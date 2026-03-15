  * tags: #fundamentals #testing #javascript #javascript #static-analysis
  * Author: [[Kent C. Dodds]]
  * Notes:
    * You can install eslint by `npm install --save-dev eslint`
      * create file `.eslintrc` in your root file of the project
      * Then you can run eslint by  `npx eslint .`
      * running script with automatic fixing `npx eslint . --fix`
    * Command + dot = automatically fix the problem with eslint
    * ### Extends
      * You don't have to specify all the rules by yourself, you can always use extends which includes set of predefined rules based on what extend you use
      * ```javascript
"extends": ["eslint:recommended"],```
    * ### Eslint Ignore
      * You can either create `.eslintignore` file, which works same way as `.gitignore`
      * Or you can use `.gitignore` even for eslint with command `"lint": "eslint --ignore-path .gitignore ."`
    * ### Prettier
      * Package for formatting your files
      * ```javascript
"format": "prettier --ignore-path .gitignore --write \"**/*.+(js|json)\""```
      * Prettier config
        * You can go here to prettier playground and set up your config as you like https://prettier.io/playground/
        * Then create file `.prettierrc`
      * Prettier config in VS-Code
        * ```javascript
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,```
      * You can install package `eslint-config-prettier` to avoid issues that prettier solves
        * Just install and add this option to `.eslintrc` `"extends": ["eslint:recommended", "eslint-config-prettier"]`
      * Validate of files are properly formatted
        * ```javascript
    "prettier": "prettier --ignore-path .gitignore \"**/*.+(js|json)\"",
    "format": "npm run prettier -- --write",
    "check-format": "npm run prettier -- --list-different",
    "validate": "npm run check-format && npm run lint && npm run build"```
        * you can see prettier command and then command that uses this command as base, plus we are providing different arguments by `--` before the actual arguments
        * `--list-different` just validates the files and throws error if you need to format them 
    * ### TypeScript
      * We have to install typescript by `npm run install --save-dev typescript`
      * Renaming our files to `.ts` and creating ts config file `tsconfig.json`
        * ```javascript
{
  "compilerOptions": {
    "noEmit": true,
    "baseUrl": "./src"
  }
}```
      * Your babel needs to support typescript as well, install `npm install --save-dev @babel/preset-typescript` and then adding to the babel presests settings
    * ### Eslint supporting typescript files
      * To support eslint in typescript files you need to install
        * ```javascript
"@typescript-eslint/eslint-plugin": "^4.14.1",
"@typescript-eslint/parser": "^4.14.1",```
      * We need to add some overrides to the `.eslintrc` file
        * ```javascript
  "overrides": [
    {
      "files": "**/*.+(ts|tsx)",
      "parser": "@typescript-eslint/parser",
      "parserOptions": {
        "project": "./tsconfig.json"
      },
      "plugins": ["@typescript-eslint/eslint-plugin"],
      "extends": [
        "plugin:@typescript-eslint/eslint-recommended",
        "plugin:@typescript-eslint/recommended",
        "eslint-config-prettier/@typescript-eslint"
      ]
    }
  ]```
      * And as last thing we extend script for linting
        * `    "lint": "eslint --ignore-path .gitignore --ext .js,.ts,.tsx .",`
    * ### Husky
      * `npm install --save-dev husky`
      * It automatically adds some git settings to your project
      * You can create settings file `.huskyrc`
        * ```javascript
{
    "hooks": {
        "pre-commit": "npm run validate"
    }
}```
      * It automatically runs npm run validate script before you commit something to your git, if this script fails, it won't commit anything
    * ### Lint-staged
      * `npm install --save-dev lint-staged`
      * Create config file `.lintstagedrc` with 
        * ```javascript
{
    "*.+(js|ts|tsx)": [
        "eslint"
    ],
    "**/*.+(js|json|ts)": [
        "prettier --write",
        "git add"
    ]
}```
        * This runs and adds to your commit all the changes made by prettier, so even people without prettier doesn't have run into the issues before committing
    * ### npm-run-all
      * `npm run install --save-dev npm-run-all`
      * and then you can run all those script in parallel
        * ```javascript
"validate": "npm-run-all --parallel check-types check-format lint build"```
