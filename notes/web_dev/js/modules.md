### Modules Overview

- Reusable pieces of code that can be exported from one program and imported for use in another program
- Benefits of Using Modules:
  - Find, fix, and debug code more easily
  - Reuse and recycle logic defined in different parts of our application
  - Keep information private and protected from other modules
  - Prevent pollution of the global namespace and potential naming collisions, by cautiously selecting variables and behavior we load into a program
- Two Ways of Implementing Modules:
  - Node.js's `module.exports` and `require()` syntax
  - ES6 `import`/`export` syntax

---

### Node.js Syntax

#### module.exports

- Every JavaScript file run in Node has a local `module` object with an `exports` property used to define what should be exported from the file
- The pattern we use to export modules:
  1. Create an object to represent the module.
  2. Add properties or methods to the module object.
  3. Export the module with `module.exports`.

```javascript
let Menu = {};
Menu.specialty = "Roasted Beet Burger with Mint Sauce";

module.exports = Menu; 
```

- Can also wrap any collection of data/functions in an object and export the object (Equivalent to above block) 

```javascript
module.exports = {
  specialty: "Roasted Beet Burger with Mint Sauce",
  getSpecialty: function() {
    return this.specialty;
  } 
}; 
```

#### require()

- Used in Node to import the exported module into another file so its defined behavior can be used
- Takes a file path argument pointing to the original module file
  - The .js extension in the file path is optional and will be assumed if not included
- The pattern to import a module:
  1. Import the module with `require()` and assign it to a local variable.
  2. Use the module and its properties within a program.

``` javascript
const Menu = require('./menu.js');

function placeOrder() {
  console.log('My order is: ' + Menu.specialty);
}
placeOrder();
```

---

### ES6 Syntax

#### export default

- Works similarly to the `module.exports` syntax, allowing us to export 1 module per file
- Not supported in Node.js so this syntax is used for front-end development 

``` javascript
let Menu = {};
export default Menu; 
```

#### import

- The name following `import` specifies the name of the variable to store the default export in 
- When specifying the path name after `from`, .js is left off because it specifically refers to the name of the file w/o the extension of the file when dealing with local files

```javascript
import Menu from './menu';
```

#### Named Exports

- Allow us to export data through the use of variables

```javascript
let specialty = '';
function isVegetarian() {}; 

export { specialty, isVegetarian };
```

- Named exports can have their name changed when exported using `as`

```javascript
let specialty = '';
let isVegetarian = function() {}; 

export { specialty as chefsSpecial, isVegetarian as isVeg };
```

- Variables can be exported as soon as they are declared by placing `export` in front of variable declarations

```javascript
export let specialty = '';
export function isVegetarian() {}; 
```

- Named exports and default exports can be used together 
  - Best not to use both methods but can occasionally be useful
    - Ex: If you suspect developers may only be interested in importing a specific function and won’t need to import the entire default export. 

```javascript
let specialty = '';
function isVegetarian() {};  
function isGlutenFree() {};

export { specialty as chefsSpecial, isVegetarian as isVeg };
export default isGlutenFree;
```



#### Named Imports

- To import objects stored in a variable, we use the `import` keyword and include the variables in a set of `{}`
  - Don't have to import all the variables exported in the other module

```javascript
import { specialty, isVegetarian } from './menu';
console.log(specialty);
```

- Named exports can have their name changed when exported/imported using `as`

```javascript
import {speciality as chefsSpecial, isVegetarian as isVeg} from './menu';
//or
import * as Carte from './menu';
Carte.speciality;
Carte.isVegetarian();
```

- Named imports and normal imports can be used together

```javascript
import { specialty, isVegetarian } from './menu';
import GlutenFree from './menu';
```

