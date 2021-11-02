# Steps to intialize NodeJS project with Express JS and TypeScipt

___

>
> 👀 **Prerequisite:**
> It is suggested that you should initialize your project with JavaScript first, then move to TypeScipt so it won't cause your any problem during testing process.
>

## 1. Initialize Node project

```bash
yarn init
```

or

```bash
npm init --yes
```

## 2. Add Express JS

```bash
yarn add express
```

or

```bash
npm install --save-dev express
```

>
> 💡 **Note:** You can specify prefer version of dependencies, I will just leave version option blank so Yarn or NPM will pick the last version.
>

***Test the installation:***
In order to test the installation of Express, create a new file names `index.js` in your project's root directory and add the following lines.

```Javascript
const express = require('express');
const app = express();
const PORT = 8000;

app.get('/', (req,res) => res.send('Express + TypeScript Server'));
app.listen(PORT, () => {
  console.log(`⚡️[server]: Server is running at https://localhost:${PORT}`);
});
```

Then run this command in your preferred shell.

```bash
node index.js
```

If no warning shown in the console, then you are good to go.

## 3. Add TypeScript

### 3.1. Add typescript dependencies

There are two required dependencies for TypeScript to work properly with your installed project:

- `typescript` is a core library that helps to compile the TypeScript code to valid JavaScript
- `ts-node` is a utility library that helps to run a development server written using TypeScript directly from the terminal

Both of them can be installed using a single command:

```Bash
yarn add -D typescript ts-node

```

Next, create a tsconfig.json file at the root of the development server project. This file allows you to customize TypeScript configuration and add other configurations to compile the TypeScript project:

```json
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "rootDir": "./",
    "outDir": "./build",
    "esModuleInterop": true,
    "strict": true
  }
}

```

The compilerOptions is a mandatory field that needs to be specified. The options used in the config above are:

- `target` allows us to specify the target JavaScript version that compiler will output
- `module` allows us to use a module manager in the compiled JavaScript code. The `commonjs` is supported and is a standard in Node.js
- `rootDir` is an option that specifies where the TypeScript files are located inside the Node.js project
- `outDir` specifies where the output of the compiled is going to be located
- `esModuleInterop` allows us to compile ES6 modules to `commonjs` modules
- `strict` is an option that enables strict type-checking options

There might be other configuration options that you can add on for the TypeScript compiler but these are the basic configuration options specified that can help you to get started.

### 3.2. Install declaration files for Node.js and Express

Declaration files are predefined modules that describe the shape of JavaScript values (the types present) for the TypeScript compiler. Type declarations are usually contained in files with a `.d.ts` extension. These declaration files are available for all libraries that are originally written in JavaScript and not TypeScript.

There is a GitHub repository that maintains the TypeScript type definitions to use directly in Node.js and other JavaScript projects without bothering to define these types from scratch. This repository is called [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped).

To add these types or the declaration files related to a particular library or a module, you have to look for the packages that start with `@types` namespace.

For example, the type definitions for Express library is kept under a specific package called `@types/express`. For using a utility library such as `bodyParser` (which is a middleware to parse an incoming request’s body), there is a specific type of definition module called `@types/body-parser`.

To install type definitions for Node.js and Express, run the below command. Do note that, these type definitions are installed as devDependencies:

```bash
yarn add -D @types/node @types/express
```

### 3.3. Create an Express server with .ts extension

Now you can easily convert the minimal server code in `index.js` to `index.ts` file. That is the first step. Rename the file to `index.ts.`

The `.ts` extension is a file extension to determine the TypeScript files that are compiled to JavaScript files later when building the server.

Open `index.ts` file. You can now use the import statements from ES6. The only required package right now in the `index.ts` file is `express`. Replace it with the following statement:

```typescript
import express from 'express';

const app = express();
const PORT = 8000; // This should be changed to your per deployment environment variable

app.get('/', (req, res) => res.send('Express + TypeScript Server'));
app.listen(PORT, () => {
  console.log(`⚡️[server]: Server is running at https://localhost:${PORT}`);
});
```

### 3.4. Watching file changes with nodemon

Another development related utility library I like to use when working on Node.js projects is `nodemon`. Let’s install this using the command below:

```bash
yarn add -D nodemon

```

`nodemon` is a tool that helps develop Node.js based applications by automatically restarting the Node application when file changes in the directory are detected. To use it, you may add a `start` script in the `package.json` file as specified below:

```json
"scripts": {
  "start": "nodemon index.ts",
},
```

Now, go back to the terminal window, and run `yarn start` or `npm start`.

## 4. Post installation

### 4.1 Compile a TypeScript project

To compile a TypeScript project to a valid JavaScript one, start by declaring a new script called build inside the package.json file:

```json
"scripts": {
  "build": "tsc --project ./",
},
```

TypeScript provides a command to compile the code called `tsc`. This command demands a flag to specify as to what to compile. The `--project` (shorthand: `-p`) is used to specify the project directory that the compiler can pick the code files from to compile to valid JavaScript. The `./` specifies the root project.

From the terminal window, run the build command to compile the code:

```bash
yarn run build
```

There is a new `build` directory created after this command executes successfully. Inside this directory, there is the TypeScript code compiled to valid JavaScript:

If you specify any other directory named as the value of the property `outDir` in the `tsconfig.json` file that name of the directory would have reflected here instead of `build`.
