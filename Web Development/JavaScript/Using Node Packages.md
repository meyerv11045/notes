### Using Node Packages in a Project

1. Initialize the project with `npm init`

2. Install the desired packages with `npm i package` 

   -  `-D` flag (Shorthand for `--save-dev`) is used to save packages for necessary for development purposes (e.g. unit tests, minification, etc. )
     - Saves the package to `"devDependencies"` in package.json

   - `-S` flag (Shorthand for --save) is used to save packages required for the application to run
     - Saves them to `"dependencies"` in package.json
     - Automatically saves new packages in npm 5+

3. Edit the `"scripts"` object in **package.json** to include necessary commands 

4. Run the scripts using `npm run script_name`

---

### Scripts:

##### Sass (CSS Pre-Compiler): 

- `node-sass` package should be saved to devDependencies

```json
"sass": "node-sass -w scss/ -o dist/css/ --recursive" 
```

- Command watches (-w) the scss folder and outputs (-o) the compiled css to the css folder in the dist directory 
- --recursive prevets issues with partials and auto-reloading 

##### Jest (JS Testing Framework):

- `jest` package should be saved to devDependencies

```json
"test": "jest"
```

##### Babel (ES6+ to ES5 Transpilation):

- `babel-cli` and `babel-preset-env` packes should be saved to devDependencies

```json
"build": "babel src -d lib"
```

