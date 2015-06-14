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
  .then(value => console.log(value))

  // => ...<3 seconds>... ['yo', 'yo']
```
> Aha! Promises can hold asynchronous values!


```js
new Promise(resolve => resolve(1))
  .then(number => number + 1)
  .then(number => console.log(number)) // => 2
```
> The last thing we should know about promises is `.then` === `.map`


## Reflection

Promises are a type that represents (asynchronous) values that can fail.
> Generic Data <-> String | Ordered data <-> Array
  | Asynchronous Data <-> Promise



# Usage


```js
const one = fetch('/api/v1/one').then(response => response.json())
const two = fetch('/api/v1/two').then(response => response.json())

const three = one
  .then(x => two
    .then(y => x + y))

three.then(console.log) // => 3 
```
> At this point all we can do is play around with promise-wrapped values to help
  us gain a more firm intuition as to their utility.


```js
/**
 * @summary Promise<number> -> Promise<number> -> Promise<number>
 */
const add = (numOne, numTwo) => numOne
  .then(x => numTwo
    .then(y => x + y))

const three = add(one, two)

three.then(console.log) // => 3
```
> We can use the same abstraction intuitions we know and love on this new type 
  create functions that we can use to consume and compose!


```js
const numbers = [
  fetch('/api/v1/one').then(response => response.json()),
  fetch('/api/v1/two').then(response => response.json()),
  fetch('/api/v1/three').then(response => response.json()),
  fetch('/api/v1/four').then(response => response.json()),
]

const add = (numOne, numTwo) => numOne
  .then(x => numTwo
    .then(y => x + y))

numbers
  .reduce(add, Promise.resolve(0))
  .then(console.log) // => 10
```
> Gettin' fancy with it. Because promises are just types we can use them like
  we would any other!



# Getting Lifted
> So let's think a bit more critically about asynchronicity in our programs


## A complex timeline
```
async - - - - - - - - - - - - - - - - - - - - - - - - - - ->
      ^           |^       |^     |^                      |
      |           ||       ||     ||                      |
      |           v|       v|     v|                      v
sync  ----------------------------------------------------->
                            time
```
> Here's a simple diagram of the dance we typically do to unify sync and async
  values. We could do better.


# Mathematical!
```js
1/2 + 1/6
```
> How do I add two fractions with different denominators?


```js
3/6 + 1/6 === 4/6
          === 2/3
```
> LCD: Lowest common denominator.


## Lowest common abstraction

```js
const one = fetch('/api/v1/one').then(response => response.json())
const two = 2
```
> How can I add the potential value of 1 with the available value of 2?


"An asynchronous value is not available now but a synchronous value will exist
later." - Talon


```js
const one = fetch('/api/v1/one').then(response => response.json())
const two = 2

add(one, Promise.resolve(2))
```


## Namaste
```
async - - - - - - - - - - - - - - - - - - - - - - - - - - ->
      ^                                                   |
      |                                                   |
      |                                                   v
sync  ----------------------------------------------------->
                            time
```



# Thank you

<a href='http://twitter.com/legittalon'>@legittalon</a>
