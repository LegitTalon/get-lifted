# Get Lifted
A Talk About JavaScript Promises

<a href='http://twitter.com/legittalon'>@legittalon</a>



## *Question*: What is a Promise?

<span class="fragment">*Answer*: A type.</span>
> Promises are *just* a type, homie



# Intuition
> How do I represent generic data?


```js
const word = new String('hello')
```
> Strings are a type that represent generic data.


```js
const reversed = string => string
  .split('') // new Array('h','e','l','l','o') 
  .reverse() // new Array('o','l','l','e','h')
  .join('')  // new String('olleh')
```
> When I want to reverse the string I turn it into an array 'cause Arrays are 
  good for iterating over stuff and being ordered. Strings know how to become 
  arrays know how to become strings.


```js
console.log(
  reverse(new String('{^%34')) // => '43%^{'
)
```
> Generic data, reversed! 


```js
const words = new Array(new String('hello'), new String('bye'))
```
> How do I reverse a bunch of words?


```js
const words = new Array(new String('hello'), new String('bye'))
const reversedWords = words.map(reverse)
```
> Actually, how do I transform the value of an array? use `.map`


## Reflection

Types encapsulate data inside laws.
> We classify data into types to provide it with special properties or laws,
  binary trees, weakmap, map, array, promise, etc.



## Intuition, revenge of

```js
Promise
```
> Let's play with this new type.


```js
new Promise(resolve => resolve('hello'))
  .then(value => console.log(value)) // => 'hello'
```
> So I construct this type with a function. I am given `resolve`. Resolved
  values are available via `.then` 


```js
new Promise((resolve, reject) => reject('hello'))
  .then(value => console.log(value))
  .catch(value => console.log(value)) // => 'hello'
```
> Optionally I am also given a `reject` function. Rejected values are only 
  available via `.catch`


```js
new Promise(resolve => resolve('hello'))
  .catch(value => console.log(value))
```
> So promises can be used for forking my code! But what are the some other
  implications?


```js
new Promise(resolve => setTimeout(() => resolve(['yo', 'yo']), 3000))
  .then(value => console.log(value)) // => ...<3 seconds>... ['yo', 'yo']
```
> Aha! Promises can hold asynchronous values!


## Reflection

Promises represent, potentially asynchronous, values that can fail.
