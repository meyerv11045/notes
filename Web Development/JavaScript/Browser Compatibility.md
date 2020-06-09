### Browser Compatibility

- Some ES6 features, like modules, are still not supported by most web browsers
- [caniuse.com](http://caniuse.com/) is the bset resource for finding browser compatiblity info on a feature-by-feature basis
- ES5 updated to ES6:
  - Better readability and requires fewer characters
  - Fixes ES5 bugs common from the syntax
  - Syntax more similar to other OOP languages
- Ecma (Organization in charge of JS standards) made ES6 backwards compatible meaning it can be mapped to ES5
  - Backwards compatibility helps decrease browser compatibility issues
- **Babel** is a library that *transpiles* ES6 to ES5 JavaScript
  - Transpilation- the process of converting one programming language to another
  - `babel-cli`- Node package w/ command line tools for Babel
  - `babel-preset-env`- Node package w/ ES6+ to ES5 syntax mapping information

---

#### Transpilation (Detailed Notes)

1. Setup the project using the specified file structure and npm

   ```bash
   project
   |_ src
   |___ main.js
   |_ package.json
   ```

   - Run `npm init` to create a **package.json** file in the root directory that contains info about the current project:
     - Metdata- Project Title, Description, Authors, etc
     - List of Required Node Packages- npm downloads the packages in this list when other developers want to run your project
     - Key-value pairs for command line scripts- can use npm to run these shorthand scripts to perform some process

2. Install necessary Babel packages using node package manager (npm)

   ```bash
   npm install babel-cli -D
   npm install babel-preset-env -D
   ```

   - `install` creates a folder called **node_modules** and copies the package files to it while also installing all the dependencies for the given package
   - `-D` flag instructs npm to add each package to a property called `devDependencies` in **package.json** 
     - `devDependencies` allows other developers to run your project without installing each package separately 
     - Instead they can run `npm install` to instruct npm to look inside **package.json** and download all the packages listed in `devDependencies`
   - New Directory Structure: (`...` indicates 100+ packages that npm installed)

   ```bash
   project
   |_ node_modules
   |___ .bin
   |___ ...
   |_ src
   |___ main.js
   |_ package.json
   ```

3. Specify the initial JS version in **.babelrc**

   -  Run `touch .babelrc` in the root directory to create the file
   - Define the preset for the source JS file (`["env"]` insrtucts Babel to transpile any code from ES6+)

   ```
   {
   	"presets": ["env"]
   }
   ```

4. Specify a script in **package.json** that initiates ES6+ to ES5 transpilation

   - In the "scripts" object, add a property called "build" below "test"
   - `"build"`'s value (`babel src -d lib`) is a command line method that trasnpiles ES6+ code to ES5 
     - `babel` — The Babel command call responsible for transpiling code.
     - `src` — Instructs Babel to transpile all JavaScript code inside the **src** directory.
     - `-d` — Instructs Babel to write the transpiled code to a directory.
     - `lib` — Babel writes the transpiled code to a directory called `lib`.

   ```json
   ...
   "scripts": {
     "test": "echo \"Error: no test specified\" && exit 1",
     "build": "babel src -d lib"
   }, ...
   ```

5. Type `npm run build` to build the transpile the code to ES5 where it is stored in a directory called **lib** as a file with the same name as the original file (./lib/main.js)

   - The command runs the `build` script in **package.json**
   - The one command transpiles all code in **src**- good for larger projects with numerous JS files

---

#### Transpilation Process (Summary):

1. Initialize your project using `npm init` and create a directory called **src**

2. Install babel dependencies by running

   ```
   npm install babel-cli -D
   npm install babel-preset-env -D
   ```

3. Create a **.babelrc** file inside your project and add the following code inside it:

   ```
   {
     "presets": ["env"]
   }
   ```

4. Add the following script to your `scripts` object in package.json:

   ```json
   "build": "babel src -d lib"
   ```

5. Run `npm run build` whenever you want to transpile your code from your **src** to **lib** directories