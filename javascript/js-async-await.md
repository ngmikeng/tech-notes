JS Async & Await
===

## Async
- The `async` keyword will be define before a function.

```js
async function hello() {
  return "I am a promise resolved";
}
```
- A function with `async` before will always return a promise.
```
hello().then(res => console.log(res)) // "I am a promise resolved"
```
- If throw an error inside `async function` that is equivalent to `Promise.reject()` and the end result will jumb to the `catch` block.
- A function with `async` before will be able use `await` inside to handle result of an asynchronous function.

## Await
- The `await` keyword will be define before an asynchronous function or a promise.
- Make the code wait until a promise resolve or an asynchronous functiom return a result.
- Unable use outside `async function`.

```js
async function hello() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 1000)
  });
  
  let result = await promise; // wait till the promise resolves (*)

  return result;
}
```

- Able use in top-level by hack code: use inside an immediately-invoked function,...

```js
(async () => {
	await Promise.resolve(100);
})();
```

- Use `try catch` block to handle errors of `await` functions.

```js
async function hello() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("done!"), 1000)
  });
  
  try {
  	let result = await promise; // wait till the promise resolves (*)
  } catch (err) {
  	throw err;
  }

  return result;
}
```

## References
- Basic knowledge
https://javascript.info/async-await
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function
- Use await in top-level code
https://github.com/tc39/ecmascript-asyncawait/issues/9
https://gist.github.com/Rich-Harris/0b6f317657f5167663b493c722647221