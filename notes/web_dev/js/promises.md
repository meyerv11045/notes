### Ayscnhronous Programming

- An *asynchronous operation* is one that allows the computer to “move on” to other tasks while waiting for the asynchronous operation to complete
- Asynchronous programming means that time-consuming operations don’t have to bring everything else in our programs to a halt
- JS handles asynchronicity using the `Promise` object, introduced with ES6 

---

### What is a Promise?

- Promises are objects that represent the eventual outcome of an asynchronous operation 
- A `Promise` object can be in one of three states:
  - **Pending**: The initial state— the operation has not completed yet.
  - **Fulfilled**: The operation has completed successfully and the promise now has a *resolved value*. For example, a request’s promise might resolve with a JSON object as its value.
  - **Rejected**: The operation has failed and the promise has a reason for the failure. This reason is usually an `Error` of some kind.
- A promise is *settled* if it is no longer pending (it is either fufilled or rejected)
- All promises eventually settle
  - Enables us to write logic for what to do if the promise fulfills or is rejected
- Promises are returned from a asyncrhonous operations

---

### Constructing a Promise Object

- `Promise` constructor takes a function called the *executor function* as an argument
- *Executor Function* runs automatically when constructor is called, generally starts an asynchronous operation, and dictates how the promsie should be settled
  - Has 2 function parameters: `resolve()` and `reject()` (These functions aren't defined by the progammer but are rather passed by JS into the executor function when the `Promise` constructor runs)
- `resolve` has one argument and will change the promise's status from `pending` to `fulfilled` if invoked and will set the resolved value to the argument passed in
- `reject` takes a reason or error as an argument and will change the promise's status from `pending` to `rejected` if invoked and will set the rejection's reason to the argument passed in
- Promises settle based on the results of an asynch operation (e.g. Database request is fulfilled with data from the query or is rejected with an error thrown)

```javascript
const executorFunction = (resolve,reject) => {
  if (condition){
    resolve('Say Something')
  }
  else {
		reject('Say a different thing')
  }
}
const myPromise = new Promise(executorFunction)
```

### setTimeout() in Node:

- Takes a callback function and delay in milliseconds as arguments
- The callback function will execute in *at least* the passed in delay (Could be longer)
  - This happens b/c after the delay, the line of code is added to be run but any synchronous code from the program will run before it, possibly delaying the callback functions execution 
- 