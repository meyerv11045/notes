### What is JavaScript

- Dynamic Programming Language (operations done at run-time)
  - E.g. Possible to change variable type or add new properties/methods to an object while the program is running
- Dynamically-Typed Language (Interpreter assigns variables a type at runtime based on its current value)
- Can provide interactivity on websites when applied to an html document
- Interpreted language (Doesn't have to be compiled)
- Runs on the client's computer/browser
- Object Based
  - Prototype based instead of class based like Java
- Scripting language (lightweight)

---

### Uses for JavaScript:

- Put content in an HTML page on the fly
- Make webpages responsive
- Detect a user's browser and other info
- Create cookies
- Validate forms
- Create animations, slideshows, scrollers, etc
- Build apps w/ JS frameworks (ex: angularJS, reactJS, etc)

---

### Primitive Data Types

- Number- integers and decimals
- String- use single or double quotes (single preferred)
  - `.length` property
- Boolean- `true` or `false`
- Null- intentional absence of a value represnted by `null`
- Undefined- absence of a valuae represented by `undefined` and is different than `null`
- Symbol- unique identifiers and useful in more complex coding

---

### Variables

- When declaring variables without assigning a value, their inital value is set to `undefined`
- Prior to ES6, `var` was the only keyword to declare variables ([More Info](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var))
  - Variables declared using `var` are created before any code is executed in a process known as hoisting
    - A variable's initial value is `undefined` and its actual value is intialized when the assignment statement is reached in execution
  - This means a variable can be used before it is declared in the code since hoisting results in the equivalent of all variables being declared at the top
- In ES6, `let` and `const` were introduced
  - `let` signals that the variable can be reassigned a different value
  - `const` signals that the variable is a constant and cannot be reassigned 
    - Reassigning a `const` will throw a `TypeError`
- Variables can be transformed using mathematical asignment operators (`+=`,`*=`,` /=`) and increment/decrement operators (`++`,`--`)
- In ES6, we can insert (or interpolate) variables into strings using *template literals* 
  - Uses backticks instead of single/double quotes

```javascript
const myPet = 'armadillo';
console.log(`I own a pet ${myPet}`);
// Output: I own a pet armadillo.
```

- `typeof` operator will return a string of the data type of the value to its right (e.g. typeof 'hello' returns 'string') 

---

### Conditional Statements

``` javascript
if (greeting) {
	console.log('Hello World!')
} else if (goodbye){
	console.log('Bye World!')           
} else {
  console.log('IDK')
}
```

- Comparison Operators: `<` ,` >`,` <=`,` >=`,` ===`,` !==`
  - Don't use `==` or `!=` b/c types are not considered [(Read More)](https://stackoverflow.com/questions/359494/which-equals-operator-vs-should-be-used-in-javascript-comparisons)
- Logical Operators: and `&&`, or `||`, not: `!`
- Values that are not explicitly true/false but evaluate to true/false are called truthy/falsy
  - Falsy: `0`,empty strings, `null`, `undefined`, `NaN`
  - Truthy: If a variable's value exists, it evaluates to true in a logical comparison

``` javascript
let defaultName;
if (username) {
	defaultName = username;
} else {
	defaultName = 'Stranger';
}
//Is equivalent to 
let defaultName = username || 'Stranger'; //Stranger is the default if usrname is falsy (DNE)
```

- A ternary operator can condense if...else statements
  - If the condition before the `?` is true, the 1st expression executes. If false, the 2nd expression executes

```` javascript
let isNight = true;
if (isNight){
  console.log('Sleep')
} else {
  console.log('Wakeup')
}
//Is equivalent to:
isNight ? console.log('Sleep') : console.log('Wakeup');
````

- Supports `switch` statements for easier syntax than numerous `else if` statements

``` javascript
let item = 'Pie'
switch (item) {
  case 'bread':
		//Do something
  	break;
  case 'muffin':
    //Do something else
    break;
  default:
    //Last resort
    break;
}
```

---

### Functions

- Hoisting applies to functions as well, allowing a function to be called before it is defined in the code
  - Not good code practice though
- A function declaration binds a function to an identifier like `getUser()` using the `function` keyword
- ES6 added the ability to use default parameters

``` javascript
function calcArea(width,height=10){
	return width * height;
}
```

- Helper functions- functions called within another function
- *Function Expressions* are another way to define a function 
  - The anonymous functions created by function expressions are stored in variables so they can be referenced
  - const is used to declare the variable

``` javascript
const calcArea = function(width,height){
	return width * height;
}
```

- ES6 introduced *arrow function syntax* as a shorter way to write functions [(Documentation)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
  - Remove the need to type out the function keyword
  - Include parameters inside the parentheses and add an arrow `=>` pointing to the function body

``` javascript
const calcArea = (width,height) => {
	return width * height;
}
```

- *Conscise Body Arrow Functions* 
  - Functions taking 1 parameter don't need parentheses but 0 & 2+ parameters require parentheses
  - Pushing the function to the single-line eliminates need for curly braces and return statement (implicitly returns the contents of the block)

``` javascript
const sumNums = num => num + num; //Will return num + num
```

---

### Scope

- Defines where variablescan be accessed or referenced
- In *block scope* variables are declared inside a block (set of `{}`) and are called *local variables*
  - Local variables can only be accessed within the block
- In *global scope* variables are declared outside of a block and are called *global variables*
  - Global variables can be accessed by any code in the program
- The *global namespace* is where global variables go and it allows them to be accessed anywhere in the program
- *Scope Pollution* occurs when too many global variables exist in the global namespace or when variables are reused across different scopes
  - Best practice not to define variables in the global scope to avoid this proble
- Scope variables as tightly as possible using block scope
  - Makes code more legible & understandable since blocks organize the code into discrete sections
  - Easier to maintain the modular code
  - Saves memory b/c the variables are automatically erased after the block is finished running

---

### Arrays

- [Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
- Can store any combination of data types( `const list = ['Hello',45,true]`)
- Traditional array access & updates(`list[0]` and `list[1] = 56`)
- Can change the contents of an array declared with `const` but cannot reassign a new array or different value to the variable
- `.length` property just like strings
- `.push(item)` adds items to the end of an array  & `.unshift(item)` adds items to the beginning ofan array
  - Can take multipe arguments to add multiple items at a time
  - Changes/mutates the original array (Also classified as a destructive array method since it changes the initial array )
- `.pop()` removes the last item of an array & `.shift()` removes the first item (Neither take any arguments)
  - Changes/mutates the original array
- `.indexOf(item)` returns the index of an item in the array (not found = -1)
- `.slice()` copies an array ( `let copy = og.slice();`)
- `.splice(pos,n)` removes the item at `pos` `n` times
  - Changes the original array and returns the removed items as another array
- *Pass-by-Reference* is when an array is passed into a function, if the array is mutated inside the function, that change will be maintained outside the function as well 
  - Works because the argument to the function is just a reference to where the variable is stored in memory, allowing the memory of the array to be changed
- Nested arrays can be accessed by chaining on more bracket notation with index values (e.g. `arry[1][3]`)

```javascript
let nums = [1,5,7,3,9];
let num2 = new Array(1,3,6,'Hi',3,7);
nums.push(10);
nums.length
num2.sort() //Strings come last
nums.reverse() //Reverses order
```

---

### Loops

- for loop consists of an initialization, stopping condition, and iteration statement
- Do while loops run a piece of code then check the condition compared to while loops that check the condition and then run the code
  - Do while loops run at least once whether or not the condition evaluates to true
- `break` keyword allows programs to break out of a loop within the loop's block

``` javascript
for (let i = 0; i < 5, i++){}
for (let i = items.length - 1; i >= 0; i--){} //Reverse through a list 

while (condition) {} //Avoid infinite loops!

do {} while (condition)
```

---

### Higher-Order Functions

- Functions that accept other functions as arguments and/or return functions as output 
  - *Callback Functions* are functions that are passed as arguments and invoked 
    - Get called during the excution of the higher-order function
    - To pass a callback function as ana argument, the name is typed w/o the parentheses so that the reference to the function is passed, not the value from invoking the function
    - Anonymous functions can be passed as arguments as well (they are defined in the higher-order function's call)
- Adds another level of abstraction to a program to make it more modular & easier to read/debug
- JS functions are *first class objects* meaning that like other objects, JS functions can have properties and methods
  - Functions are special b/c they can be invoked and treated like any other type of data 
  - Every JS function is actually a `Function` object ([Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function))

---

### Iterators

- These iterators take a callback function as an argument and execute the callback function for each element in the array
- `.forEach()` 

``` javascript
const fruits = ['mango', 'papaya', 'pineapple', 'apple'];
fruits.forEach(elem=>console.log(`I want to eat a ${elem}`));
//I want to eat a mango...papaya...etc.
```

- `.map()` returns a new array unlike forEach which mutates the original array 

``` javascript
const nums = [1,2,3,4];
const bigNums = nums.map(number => number * 10); //[10,20,30,40]
```

- `.filter()` takes a boolean callback function (returns T/F) as an argument. Returns a new array 

```javascript
const favoriteWords = ['nostalgia', 'hyperbole', 'fervent', 'esoteric', 'serene'];
const longFavoriteWords = favoriteWords.filter(elem=> {
  return elem.length > 7;
});
```

- `.findIndex()`Returns the *index* of the first element that evaluates to true in the boolean callback function
  - No element that satisfies the callback returns -1 

``` javascript
const jumbledNums = [123, 25, 78, 5, 9]; 
const lessThanTen = jumbledNums.findIndex(num => {
  return num < 10;
}); //3
```

- `.reduce()` returns a single value after iterating through the elements of an array (Consists of an accumulator and iterator)
  - The optional 2nd argument sets the initial value for accumulator 

```javascript
const nums = [1,2,3,4];
const summedNums = nums.reduce((accumulator,currentVal) => {
  console.log('The value of accumulator: ', accumulator);
  console.log('The value of currentValue: ', currentValue);
  return accumulator + currentVal;
},100); //110
```

---

