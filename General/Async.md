##Async programming

###Summary
`async` functions are used to prevent the program/webapp from getting stuck whilst waiting for a function to complete. A simple example is when requesting data from an API, you want to make this function asynchronous so that the page remains responsive while the is being retrieved.

(There is a simple example at the bottom of this document)

####What is it and why use it?

Asynchronous programming is a technique that enables your program to start a potentially long-running task whilst still allowing your program to be responsive to other events while that task runs, rather than having to wait until that task has finished. Once that task is finished, your program is represented with the result.

Some examples of functions provided by browsers which can potentially take a long time (and are therefore often asynchronous) are:
- Making a HTTP request using `fetch()`
- Accessing a user's camera or microphone using `getUserMedia()`
- Asking a user to select files using `showOpenFilePicker()`

You are very likely to be required to use them correctly in many scenarios.

######Synchronous Programming
Consider the following code:
```
const name = 'Miriam';
const greeting = `Hello, my name is ${name}!`;
console.log(greeting);
// "Hello, my name is Miriam!"
```
This code:
1. Declares a string called `name`
2. Declares another string called `greeting` which uses `name`
3. Outputs the greeting to the JavaScript console.
The browser steps through the program one line at a time, in the order we wrote it. At each point, the program/browser waits for the line to finish its work before going on to the next line. It has to do this because each line depends on the work done in the preceding lines.

That makes this a **synchronous program**. It would still be synchronous even if we called a separate function, like this:
```
function makeGreeting(name) {
  return `Hello, my name is ${name}!`;
}

const name = 'Miriam';
const greeting = makeGreeting(name);
console.log(greeting);
// "Hello, my name is Miriam!"

```
Here, `makeGreeting()` is a **synchronous function** because the calles has to wait for the function to finish its work and return a value before the caller can continue.

######A long-running synchronous function
What is the synchronous function takes a long time?

The program below uses a very inefficient algorithm to generate multiple large prime numbers when a user click the "Generate primes" button. The higher the number of primes a user specifies, the longer the operation will take.

HTML:
```
<label for="quota">Number of primes:</label>
<input type="text" id="quota" name="quota" value="1000000" />

<button id="generate">Generate primes</button>
<button id="reload">Reload</button>

<div id="output"></div>

```
JavaScript:
```
const MAX_PRIME = 1000000;

function isPrime(n) {
  for (let i = 2; i <= Math.sqrt(n); i++) {
    if (n % i === 0) {
      return false;
    }
  }
  return n > 1;
}

const random = (max) => Math.floor(Math.random() * max);

function generatePrimes(quota) {
  const primes = [];
  while (primes.length < quota) {
    const candidate = random(MAX_PRIME);
    if (isPrime(candidate)) {
      primes.push(candidate);
    }
  }
  return primes;
}

const quota = document.querySelector('#quota');
const output = document.querySelector('#output');

document.querySelector('#generate').addEventListener('click', () => {
  const primes = generatePrimes(quota.value);
  output.textContent = `Finished generating ${quota.value} primes!`;
});

document.querySelector('#reload').addEventListener('click', () => {
  document.location.reload();
});

```
If a user inputs an extremely high number here, the program will not be able to do anything else while it's generating the output.

######What do we need our program to do?
1. Start a long-running operation by calling a function
2. Have that function start the operation and return immediately, so that our program can still be responsive to other events
3. Notify us with the result of the operation when it eventually completes.

This is exactly what **asynchronous functions** can do.

Example (in JavaScript):

```
async function getData() {
  const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
  const data = await response.json();
  return data;
}

getData()
  .then(data => console.log(data))
  .catch(error => console.error(error));
```
In this example, the '**getData**' function is declared as an '**async**' function, which allows us to use the '**await**' keyword to wait for a '**Promise**' to resolve before continuing execution.

Inside the function, we use '**await**' twice to wait for the '**fetch**' call to complete and for the JSON response to be parsed. We then return the resulting data object.

Outside the function, we call '**getData**' and use '**.then()**' to log the data to the console if the Promise resolves successfully, or '**catch()**' to log any errors (to the console).

By marking the function as '**async**', we can use the '**await**' keyword to pause the execution of the function until the '**fetch**' call is completed and the response is available.





