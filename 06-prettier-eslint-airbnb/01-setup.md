# Prettier / ESLint

We want our CRA to use Prettier and ESLint with the airbnb config!

First, use `create-react-app` to create your initial application.

## Create ESLint config file

```
npx eslint --init
```

```
? How would you like to use ESLint?
  > To check syntax, find problems, and enforce code style
? What type of modules does your project use?
  > JavaScript modules (import/export)
? Which framework does your project use?
  > React
? Does your project use TypeScript?
  > No
? Where does your code run?
  > Browser
? How would you like to define a style for your project?
  > Use a popular style guide
? Which style guide do you want to follow?
  > Airbnb: https://github.com/airbnb/javascript
? What format do you want your config file to be in? ...
  > JSON
? Would you like to install them now with npm?
  > No
```

## Update ESLint config file

CRA uses some language features that may not be supported in Node / Browsers. It uses `babel` to transpile the code so that it works in these environments. We need to update the `.eslintrc.json` file that was just generated to tell the eslint parser to use `babel`.

### `.eslintrc.json`

Add the "parser" line to your `.eslintrc.json` file.

```diff
  "extends": ["plugin:react/recommended", "airbnb"],
+ "parser": "babel-eslint",
  "parserOptions": {
```

NOTE: Do not add the plus sign (+). That is just indicating what line was added.

## Install ESLint packages

You should now be able to install the eslint libraries.

```
npm install
```

## Install Prettier

```
npm i -D prettier eslint-plugin-prettier eslint-config-prettier
```

## Create Prettier config file
Create a `.prettierrc` file:
```json
{
  "printWidth": 120,
  "singleQuote": true
}
```

## Configure ESLint to use prettier

```diff
- "extends": ["plugin:react/recommended", "airbnb"],
+ "extends": ["airbnb", "prettier"],
```

```diff
- "plugins": ["react"],
+ "plugins": ["prettier"],
```

```diff
- "rules": {}
+ "rules": {
+   "prettier/prettier": "error",
+   "react/jsx-filename-extension": "off",
+   "react/prop-types": "off"
+ }
```

## VS Code Extension
Make sure the `ESLint` extension is installed.

Open VS Code Settings and set:
- Editor: Default Formatter
  - `dbaeumer.vscode-eslint`

NOTE: It is probably a good idea to restart VS Code at this point to make sure the settings take effect.

## Summary
Your CRA is now using best practices ESLint configuration!

At first you may find that it is complaining at you a lot.  Feel free to look at the documentation on each rule to understand why it is a best practice.

For example, in the following code:
```js
for (let x = 0; x < 5; x++) {
  console.log(x);
}
```

The **Problems** view shows:
```
X  Unary operator '++' used. eslint(no-plusplus)
!  Unexpected console statement. eslint(no-console)
```

I need to do something about this `no-plusplus` error.

I could refactor my code:
```diff
- for (let x = 0; x < 5; x++) {
+ for (let x = 0; x < 5; x += 1) {
```

Or I could disable the line:
```js
// eslint-disable-next-line no-plusplus
for (let x = 0; x < 5; x++) {
```

Or I could disable the rule altogether in the `.eslintrc.json` file.
```diff
rules: {
+ "no-plusplus": "off",
  "prettier/prettier": "error",
```
