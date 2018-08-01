Trick set Promise timeout with `Promise.race()`
===
A note about set timeout for a Promise by using `Promise.race()`, the content is reference from this article
https://italonascimento.github.io/applying-a-timeout-to-your-promises/

Sometimes a promise may take too long to resolve or reject, maybe it’s trying to reach a server through a poor connection, or to parse a truly big file, and our application can’t wait more than 5 seconds for a response, and if it takes more than that, we need it to timeout and reject, firing our catch callback.

#### Implement a function to handle promise timeout.
```js
// timeout-promise.js
export default const promiseTimeout = function(ms, promise){

// Create a promise that rejects in <ms> milliseconds
let timeout = new Promise((resolve, reject) => {
let id = setTimeout(() => {
  	clearTimeout(id);
  	reject('Timed out in '+ ms + 'ms.')
	}, ms)
})

// Returns a race between our timeout and the passed in promise
return Promise.race([
	promise,
	timeout
])
```

#### Using with another promise
```js
import timeoutPromise from './timeout-promise';

const doSomething = function(){
  return new Promise((resolve, reject) => {
    /* ...  */
  })
};

// Apply a timeout of 5 seconds to doSomething
let doIt = timeoutPromise(5000, doSomething())

// Wait for the promise to get resolved
doIt.then(response => {
  // Use response
})

// Wait for the promise to get rejected or timed out
doIt.catch(error => {
  // Deal with error
})
```