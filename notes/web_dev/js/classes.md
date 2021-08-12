# Classes

## Constructor 

-  JavaScript calls the `constructor()` method every time it creates a new *instance* of a class.

```javascript
class Dog {
  constructor(name) {
    this.name = name;
    this.behavior = 0;
  }
}
```

---

## Instances

- An *instance* is an object that contains the property names and methods of a class, but with unique property values.

```javascript
const halley = new Dog('Halley');
console.log(halley.name); // Output: 'Halley'
```

---

## Methods

- Class method and getter syntax is the same as it is for objects except you can not include commas between methods.

```javascript
class Dog {
  constructor(name) {
    this._name = name;
  }

  get name() {
    return this._name;
  }

  incrementBehavior() {
    this._behavior++;
  }
}
```

- *Static Methods* aren't available to instances and can only be called by the class
  - Calling static methods from an instance throws a `TypeError`

```javascript
class Animal {
  constructor(name) {
    this._name = name;
    this._behavior = 0;
  }

  static generateName() {
    const names = ['Angel', 'Spike', 'Buffy', 'Willow', 'Tara'];
    const randomNumber = Math.floor(Math.random()*5);
    return names[randomNumber];
  }
} 

console.log(Animal.generateName()); // returns a name

```
---

## Inheritance

- Create a *parent* class (also known as a superclass) with properties and methods that multiple *child* classes (also known as subclasses) share 
  - Child classes inherit the properties and methods from their parent class
- Benefits (time saved, readability, efficiency) grow as the number and size of subclasses increase
- Adheres to *DRY* best practice 
- JS uses `extends` keyword to extend the properties/methods of one clas to a subclass
- `super()` Calls the constructor of the parent class (with the appropriate parameters if necessary)
  - `super()` must always be called before `this` can be used to define new properties (ReferenceError will be thrown otherwise)
  - *Best Practice:* Always call `super()` on the first line of subclass constructors

```javascript
class Animal {
  constructor(name) {
    this._name = name;
    this._behavior = 0;
  }

  get name() {
    return this._name;
  }

  get behavior() {
    return this._behavior;
  }
} 

class Cat extends Animal {
  constructor(name, usesLitter) {
    super(name);
    this._usesLitter = usesLitter;
  }
}
```