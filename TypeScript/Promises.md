###Promises

####Summary
1. Promises are objects that contain information about the completion of some asynchronous code and any resulting values we want to pass in.
2. To return a promise, we use `return new Promise((resolve, reject) => {});`
3. To consume a promise we use `.then` to get the information from a promise that has been *resolved*, and `catch` to get the information from a promise that has been *rejected*.
4. You'll probably use (consume) promises more than you'll write.

#####What is a Promise in TS/JS?
JavaScript and TypeScript are single threaded, meaning that two bits of script cannot run at the same time; they have to run one after another. A Promise is an object that represents the eventual completion (or failure) of an asynchronous operation, and its resulting value.

```
var promise = new Promise(function(resolve, reject){
    //  Do something, then...

    if (/* everything worked */){
        resolve("See, it worked!");
    }
    else {
        reject(Error("It broke..."));
    }
});
```

#####A Promise exists in one of these states
- Pending: initial state, neither fulfilled nor rejected.
- Fulfilled: operation completed succesfully.
- Rejected: operation failed.

The Promise object works as proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason.

This lets asynchronous methods return values like synchronous methods: instead of immediately returning the final value, the asynchronous method returns a promise to supply the value at some point in the future.

####Using 'Then' (Promise Chaining)
To take several asynchronous calls and synchronize them one after the other, you can use promise chaining. This allows using a value from the first promise in later subsequent callbacks.

Example:
```
Promise.resolve('some')
    .then(function(string) { // <-- This will happen after the above Promise resolves / is resolved
        return new Promise(function(resolve, reject){
            setTimeout(function(){
                string += 'thing';
                resolve(string);
            }, 1);
        });
    })
    .then(function(string) { // <-- This will happen after the above .then's new Promise resolves
        console.log(string); // <-- Logs 'something' to the console
    });
```

####Promise API
There are 4 static methods in the Promise class:
- Promise.resolve
- Promise.reject
- Promise.all
- Promise.race

####Promises can be chained together
When writing Promises to solve a particular problem, you can chain them together to form logic.
```
var add = function(x, y) {
    return new Promise((resolve, reject) => {
        var sum = x - y;
        if (sum) {
            resolve(sum);
        }
        else {
            reject(Error("Could not subtract the two values!"));
        }
    });
};

//  Starting promise chain
add(2,2)
    .then((added) => {
        //  added = 4
        return subtract(added, 3);
    })
    .then((subtracted) => {
        //  subtracted = 1
        return add(subtracted, 5);
    })
    .then((added) => {
        //  added = 6
        return added * 2;
    })
    .then((result) =>{
        //  result = 12
        console.log("My result is ", result);
    })
    .catch((err) => {
        //  If any part of the chain is rejected, print the error message.
        console.log(err);
    })
```
This is useful for following a *Functional Programming* paradigm. By creating functions for manipulating data you can chain them together to assemble a final result. If at any point in the chain of functions, a value is *reject*, the chain will skip to the nearest `catch()` handler.

###So how does it work?
Many things is TS/JS are objects. You can create an object a few different ways, but the most common way (in JavaScript) is with object literal syntax:
```
const myCar = {
    color: 'blue',
    type: 'sedan',
    doors: '4'
}
```
You could also create a `class` and instantiate it with the `new` keyword.
```
class Car {
    constructor(color, type, doors) {
        this.color = color;
        this.type = type;
        this.doors = doors
    }
}

const myCar = new Car('blue', 'sedan', '4');
```

A promise is simply an object that we create like the later example. We instantiate it with the `new` keyword. Instead of the three parameters we passed in to make our car, we pass in a function that takes two arguments: `resolve` and `reject`.

Ultimately, promises tell us something about the completion of the asynchronous function we returned it from-if it worked or didn't. We say the function was successful by saying the promise *resolved*, and unsuccessful by saying the promise was *reject*.

When creating a promise
`const myPromise = new Promise(function(resolve, reject) {});`
The status of this promise will be "pending".
When the promise is resolved, it's status will be "resolved".

In addition, we can pass anything we'd like to into resolve and reject. For example, we could pass an object instead of a string:
```
return new Promise((resolve, reject) => {
    if(somethingSuccessfulHappened){
        const successObject = {
            msg: 'Success',
            data, // Some data we got back
        }
        resolve(successObject);
    }
    else{
        const errorObject = {
            msg: 'An error occured',
            error, // Some error we got back
        }
        reject(errorObject);
    }
});
```

Or, as we saw earlier, we don't have to pass anything:
```
return new Promise((resolve, reject) => {
    if(somethingSuccesfulHappened){
        resolve();
    }
    else {
        reject();
    }
});
```
#####A potentially decent example of how to interpret asynchronous code:
Think of JS/TS as a single lane highway. Certain code (asynchronous code) can slide over to the shoulder to allow other code to pass it. When that asynchronous code is done, it simply returns to the roadway.

