# A simple project to start learning Typescript
This is a simple project for people starting to learn TypeScript. Is already configured, so you can jump strait to leaning.  

If you want to create your own project, follow the steps bellow.  

## Softwares needed
- A text editor (Like [Visual Studio Code](https://code.visualstudio.com/))
- [NodeJS](https://nodejs.org/en/)
- A Browser (Like [Google Chrome](https://www.google.com/intl/en-US/chrome/))

After installing all softwares mentioned above, setup your environment.
## TypeScript setup
Create a folder for your project and access it using the terminal or command prompt from your computer.  

Type the following to create a `package.json` file:

```bash
npm init -y
```  

Now, install `typescript` and `ts-node` globally (for Windows systems, remove the `sudo` keyword):  

```bash
sudo npm i -g typescript
sudo npm i -g ts-node
```  

You may need a linter that will check your code in real time and tell you if something is incorrect. For that, we're going to install `eslint` and it's dependencies. Type the following:  

```bash
npm i eslint eslint-import-resolver-typescript -D
```  

If you choose to use Visual Studio Code, you should install the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint).  

## ESLint and TypeScript configuration
After following the steps above, it's time to configure ESLint and TypeScript.  

Type the following:  

```bash
tsc --init
```  

This will create a file called `tsconfig.json`. This file is used to change TypeScript default behavior (if needed).  

Now type:  

```bash
npx eslint --init
```  

ESLint will ask some questions about your preferences. Here's the answers (use the keyboard arrows and "Enter" to choose):  

- To check syntax, find problems, and enforce code style;
- JavaScript modules (import/export);
- None of these;
- Type "y" and hit "Enter";
- Use the keyboard arrows and space to choose "Browser" and "Node";
- Use a popular style guide;
- Airbnb: https://github.com/airbnb/javascript 
- JavaScript;
- Type "y" and hit "Enter";  

This will create a file called `.eslintrc.js`. This file will change ESLint behavior. We'll need to change it for our purposes (see bellow).  

## Creating folders and changing configuration files  

Now, create two folders, one called "src" and another called "dist". The src (source) folder is we're you'll add all your TypeScript files. The "dist" (distribution) folder, is where you'll put all your other files, like HTML and CSS.

We'll configure TypeScript to compile all files from "src" folder to "dist" folder keeping the same folder structure.

If you are an experienced developer, you may use Webpack or some lib/framework that will do it automatically for you. I'm not going to talk about that here.

Please, change `.eslintrc.js` file to the following:  

```javascript
module.exports = {
  env: {
    browser: true,
    es6: true,
    node: true,
  },
  extends: [
    'airbnb-base',
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  globals: {
    Atomics: 'readonly',
    SharedArrayBuffer: 'readonly',
  },
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  plugins: [
    '@typescript-eslint',
  ],
  settings: {
    'import/resolver': {
      typescript: {}
    },
  },
  rules: {
    'no-console': 0,
    'class-methods-use-this': 0,
    'import/extensions': 0,
  },
};
```  

## Compilation using the same folder structure  

If you want TypeScript to transpile (compile) all your files using the same structure you wrote your them (folders and files), do the following.

Change `outDir` configuration in `tsconfig.json` from:

```json
// "outDir": "./",
```

to:  

```json
"outDir": "./dist",
```  

## Compilation using one big JS file    

If you want TypeScript to transpile all your code into one big javascript file. Do the following:

Change `outFile` and `module` configuration in `tsconfig.json` from:

```json
"module": "commonjs",
// ... other lines
// "outFile": "./",
```

to:  

```json
"module": "amd",
// ... other lines
"outFile": "./dist/my_big_javascript_file.js",
```  

## Hello world  

Now we're all set. So, start by creating folders or files in "src" folder. I created file called `index.ts` for testing.  

```typescript
function sayHi(name: string): string {
  return `Hi ${name}`;
}

console.log(sayHi('Otávio'));
```

You can compile one file or let TypeScript watch for files that you're changing.

To compile one file manually, type:

```bash
tsc src/index.ts
```  

Where `src/index.ts` is the path to the file you want to compile.

TypeScript can also watch for files you're changing and compile them automatically. For this, type:

```bash
tsc -w
```  

You'll see that this command won't finish, it'll keep watching files as you're changing than. This is a convenient way to work faster. To stop this command, press 'CTRL+C' on your terminal.
