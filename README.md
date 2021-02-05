# Installation With Create React App

1. Navigate to your app directory where you want to include this style configuration.

   ```bash
   npx create-react-app my-app
   cd my-app
   ```

2. Run command inside your app's root directory.

   ```bash
   # Windows
   .\eslint-prettier-config.sh
   # Mac
   exec 3<&1;bash eslint-prettier-config.sh 
   ```

3. Make selections for your preference of package manager (npm or yarn), file format (.js or .json), max-line size, and trailing commas (none, es5, all).

4. Look in your project's root directory and notice the two newly added/updated config files:
   - `.eslintrc.js` (or `.eslintrc.json`)
   - `.prettierrc.js` (or `.prettierrc.json`)

# Packages

### Main Packages

1. [ESlint](https://eslint.org/)
2. [Prettier](https://prettier.io/)

### Airbnb Configuration

1. [eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)
   - This package provides Airbnb's .eslintrc as an extensible shared config.
2. [eslint-plugin-jsx-a11y](https://github.com/evcohen/eslint-plugin-jsx-a11y) (Peer Dependency)
   - Static AST checker for accessibility rules on JSX elements.
3. [eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react) (Peer Dependency)
   - React specific linting rules for ESLint
4. [eslint-plugin-import](https://www.npmjs.com/package/eslint-plugin-import) (Peer Dependency)
   - Support linting of ES2015+ (ES6+) import/export syntax, and prevent issues with misspelling of file paths and import names.
5. [babel-eslint](https://github.com/babel/babel-eslint)
   - A wrapper for Babel's parser used for ESLint.
   - We decided to include this since [Airbnb Style Guide uses Babel](https://github.com/airbnb/javascript#airbnb-javascript-style-guide-).

### ESlint, Prettier Integration

1. [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier)
   - Runs Prettier as an ESLint rule and reports differences as individual ESLint issues.
2. [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier)
   - Turns off all rules that are unnecessary or might conflict with Prettier.

# Created Configuration Files

- Once files are created, you may edit to your liking.

### eslintrc(.js/.json)

- [more info](https://eslint.org/docs/user-guide/configuring)

```
{
"extends": [
    "airbnb",
    "plugin:prettier/recommended",
    "prettier/react"
  ],
  "env": {
    "browser": true,
    "commonjs": true,
    "es6": true,
    "jest": true,
    "node": true
  },
  "parser": "babel-eslint",
  "rules": {
    "no-console": 1,
    "no-var": 1,
    "no-unused-labels": 1,
    "no-unused-vars": [
      1,
      {
        "args": "none"
      }
    ],
    "no-unused-expressions": 1,
    "max-params": [
      1,
      4
    ],
    "max-lines": [
      1,
      {
        "max": 500,
        "skipBlankLines": true,
        "skipComments": true
      }
    ],
    "max-len": [
      1,
      {
        "code": (SET BY USER),
        "tabWidth": 2,
        "comments": (SET BY USER),
        "ignoreComments": false,
        "ignoreTrailingComments": true,
        "ignoreUrls": true,
        "ignoreStrings": true,
        "ignoreTemplateLiterals": true,
        "ignoreRegExpLiterals": true
      }
    ],
    "prefer-const": 1,
    "semi": 1,
    "quotes": [
       2,
       "single",
       {
          "avoidEscape": true,
          "allowTemplateLiterals": true
          }
    ],
    "import/prefer-default-export": 0,
    "import/no-named-as-default": 0,
    "import/no-named-as-default-member": 0,
    "react/display-name": 1,
    "react/no-array-index-key": 0,
    "react/react-in-jsx-scope": 0,
    "react/prefer-stateless-function": 0,
    "react/forbid-prop-types": 0,
    "react/no-unescaped-entities": 0,
    "react/jsx-filename-extension": [
      1,
      {
        "extensions": [".js", ".jsx"]
      }
    ],
    "jsx-a11y/accessible-emoji": 0,
    "jsx-a11y/label-has-associated-control": [
      "error",
      {
        "assert": "either"
      }
    ],
    "jsx-a11y/href-no-hash": 0
  }
}
```

### prettierrc(.js/.json)

- [more Info](https://prettier.io/docs/en/configuration.html)

```
{
   "printWidth": (SET BY USER),
   "singleQuote": true,
   "trailingComma": (SET BY USER)
}
```

### package.json

- You can add two scripts to your package.json to lint and/or fix:

```
{
   "scripts": {
      "lint": "eslint .",
      "lint:fix": "eslint . --fix"
   },
}
```

- Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`. You probably want your editor to do this though.

# With VC Code

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the Open (Open Settings) icon in the top right corner:

```
{
   // These are all my auto-save configs
   "editor.formatOnSave": true,
   // turn it off for JS and JSX, we will do this via eslint
   "[javascript]": {
      "editor.formatOnSave": false
   },
   "[javascriptreact]": {
      "editor.formatOnSave": false
   },
   // show eslint icon at bottom toolbar
   "eslint.alwaysShowStatus": true,
   // tell the ESLint plugin to run on save
   "editor.codeActionsOnSave": {
      "source.fixAll": true
   }
}
```

3. After attempting to lint your file for the first time, you may need to click on 'ESLint' in the bottom right and select 'Allow Everywhere' in the alert window.
4. Finally you'll usually need to restart VS code. They say you don't need to, but it's never worked for me until I restart.

---
