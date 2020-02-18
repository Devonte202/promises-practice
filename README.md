# Unit 6 Lesson 1 Practice: Promises

## Directions
Fork and clone this lab. Respond to questions in clear, concise sentences directly within this markdown file.

**1. What will the following code snippet log? Why?**
  ```javascript
  console.log('Line 1')
  setTimeout(() => console.log('Line 2'), 1000)
  console.log('Line 3')
  ```
  This code will log:
                     Line 1
                     Line 3
                     Line 2
                     
  This is because setTimeout is an asyncronous function, therefore the code continues to execute even the that function must wait one second before logging.

**2. What does the following code snippet log? Why?**
  ```javascript
  function createPromise(seconds) {
    return new Promise((resolve) => {
      setTimeout(function() {
        resolve(`After ${seconds} second(s), this promise is resolved.`)
      }, seconds * 1000)
    })
  }

  console.log(createPromise(1000))
  ```
  The code above logs a promise object with a status of pending, because its set to be resolved after 1000 seconds, thus we still receive an object because this is an asycronous process and the code will pass us an object that will dynamically change status after it is resolved. 
  

**3. How do we use our `createPromise` function to log `"After 1 second(s), this promise is resolved."`**
```javascript
console.log(createPromise(1))
```

**4. What does the following code snippet return? What does it log?**
  ```javascript
  const ourPromise = new Promise((resolve) => {
    resolve(12);
  })

  ourPromise.then(value => value * 2);
  ```
  This code creates a new instance of a promise the resolves with a value of 12. This value is then evaluated by our then method and multiplied by two.

**5. What does the following code snippet return? What does it log?** <br> _**Note:** Instead of using the `Promise` constructor to create a Promise that immediately resolves to 12, we can just use the [`Promise.resolve`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve) method._
  ```javascript
  const ourPromise = Promise.resolve(12);
  ourPromise.then(value => value * 2).then(value => value + 10);
  ```
  Promise.resolve() allows us to create a orimise that immediately resolves to the value it's passed. Then that value is evaluated by our chained then methods, which gives us a final value of 34.

**6. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => console.log(value + 10))
  ```
  In the code above we console.log a value of 34 and return promise that has been resolved, however there is no way to reference the value of the promise because we did not return it, we only logged it.

**7. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.resolve(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    });
  ```
  In the code above we console.log a value of 34 and return that same value which gives us a promise that has been resolved, which also has a value of 34 because we returned it.
  

**8. What does the following code snippet return? What does it log? How does this differ from the question above?**
  ```javascript
  Promise.reject(12).then(value => value * 2).then(value => {
    console.log(value + 10);
    return value + 10;
    }).catch(reason => {
      const message = `${reason} is a bad number.`;
      console.error(message);
      return reason;
    });
  ```
  This code immediately rejects and returns a promise that is resolved because our catch method logs an error and returns a new promise that is successfuly resolved.