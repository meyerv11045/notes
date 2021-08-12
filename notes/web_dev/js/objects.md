## Objects

- Are *passed by reference* meaning the variable assigned to an object points to the space in memory holding the object when passed into a function as an argument
  - Functions that change object properties actually mutate the object permanently even when assigned to a `const` variable
- Can be iterated through using the `for...in` syntax that executes a given block of code for each property in an object ([Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in))

```javascript
for (let member in spaceship.crew) {}
```

---

## Object Literal

- Data is organized into key-value pairs where a key points to a location in memory that holds a value
  - Keys are strings but values can be any data type
  - When the keys don't have special characters, JS allows the quotation marks to be omitted
- Key serves as a method's name and the value is an anonymous function expression
  - ES6 syntax allows omission of the colon and `function` keyword

```javascript
let person = {
  firstName: 'John',
  secondName: 'Doe',
  age: 30,
  children: ['Bob','Joe']
  //Embedded Object
  address : {
    street: '555 Heaven Ave',
    city: 'Boston',
    state: 'MA'
  },
  fullName: function(){
    return this.firstname + ' ' + this.lastName;
  }
	//Same as
	fullName2 () {
 		console.log(this.firstname)
  }
}
```
- There are 2 notations used for accessing object properties: dot and bracket
- Braket notation must be used when accessing keys that have numbers, spaces, or special characters
- Also used for property assignment/creation
  - Can't reassign an object declared with `const`
- `delete` operator is used to delete properties

```javascript
//Dot Notation
person.age; 
person.children[0];
person.address.street;
//Bracket Notation
property = 'age';
person[property];
person['children'][0];
person['address']['street'];
```

---

## Object Constructor

```javascript
let apple = new Object();
apple.color = 'red';
apple.shape = 'round';
apple.describe = function(){
  return "Color: " +this.color+' Shape: '+this.shape;
}
```
### Constructor Pattern:

```javascript
function Fruit(name,color,shape){
  this.name = name;
  this.color = color;
  this.shape = shape;
  this.describe = function(){
    return "This is "+this.color;
  }
}
let apple = new Fruit('apple','red','round');
```

---

### `this` Keyword

- Similar functionality to `self` keyword used for clases in python
- Used to reference other properties/methods of an object from within the object
  - `this` references the *calling object* which provides access to the calling object's properties
  - A `ReferenceError` is thrown if `this` is not used

``` javascript
const goat = {
  dietType: 'herbivore',
  diet() {
    console.log(this.dietType); 
  }
};
goat.diet(); //Output: herbivore
```

- arrow functions bind/tie `this` to the function itself, not the calling object 
  - In the below example, the value of `this` is the global object (an object that exists in the global scope), which doesn't have a `dietType` property, therefore returnining `undefined`
  - *Avoid* using arrow functions when using `this` in a method

``` javascript
const goat = {
  dietType: 'herbivore',
  diet: () => {
    console.log(this.dietType);
  }
};
goat.diet(); // Prints undefined
```

---

## Privacy

- Only certain properties should be mutable/able to change in value
- JS does not have privacy built-in for objects
- Naming conventions indicate how a developer should interact with a property 
  - Underscores `_` before the name of a property: do not alter
- *Getters* are used to return internal properties of an object
  - Syntax: `get` keyword followed by a function(){}
  - Can perform an action on the data when getting a property
  - Can return different values using conditionals
  - Easier readability

```javascript
const person = {
  _firstName: 'John',
  _lastName: 'Doe',
  get fullName() {
    if (this._firstName && this._lastName){
      return `${this._firstName} ${this._lastName}`;
    } else {
      return 'Missing a first name or a last name.';
    }
  }
}
//Using a Getter
person.fullName; // 'John Doe'
```

- *Setters* are used to reassign values of an object's properties

```javascript
const person = {
  _age: 37,
  set age(newAge){
    if (typeof newAge === 'number'){
      this._age = newAge;
    } else {
      console.log('You must assign a number to age');
    }
  }
};

//Using a Setter
person.age = 40
console.log(person._age) //40 
```

---

## Factory Functions

- Returns an object that can be reused to make multiple object instances
  - Simply returns an object
- Can have parameters allowing customization of the returned object

```javascript
const monsterFactory = (name, age, energySource, catchPhrase) => {
  return { 
    name: name,
    age: age, 
    energySource: energySource,
    scare() {
      console.log(catchPhrase);
    } 
  }
};	
const ghost = monsterFactory('Ghouly', 251, 'ectoplasm', 'BOO!');
ghost.scare(); // 'BOO!'
```

---

## Destructuring

- An ES6 shortcut for assigning an object's properties to variables
- *Property Value Shorthand* can be used in creating factory functions where the property's name is the same as the variable it is being assigned to 

```javascript
const monsterFactory = (name, age) => {
  return { 
    name,
    age 
  }
};
```

- *Destructured Assignment* is similar to unpacking in python where an object's properties can be concisely assigned to new variables

```javascript
const vampire = {
  name: 'Dracula',
  residence: 'Transylvania',
  preferences: {
    day: 'stay inside',
    night: 'satisfy appetite'
  }
};

const {residence} = vampire; //Transylvania
const {day} = vampire.preferences //Stay inside

```

---

## Built-In Object Methods

- Object Instance Methods: [(Documentation)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object#Methods)
  - `.hasOwnProperty()`, `.valueOf()`
- Object Class Methods:
  - `Object.keys(name_of_obj)`: Returns an array of the keys/property names of an object
  - `Object.entries(name_of_obj)`: Returns an array containing arrays that have the key & value for each property
  - `Object.assign(target_obj,src_object)`: Copies properties from the source object (s) to the target object and returns the target object 

