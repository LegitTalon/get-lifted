# Get Lifted
A Talk About JavaScript Promises

by [@legittalon][twitter]

[twitter]: https://twitter.com/legittalon

> Introduce yoself



## *Question*: What is a Promise?

<span class="fragment">*Answer*: A structure.</span>

> Promises are *just* structures, homie



# Intuition

> How do I represent generic data?


```js
const word = new String('hello')
```

> Strings are a structure that represent generic data.


```js
const reverse = string => string
  .split('') // new Array('h','e','l','l','o') 
  .reverse() // new Array('o','l','l','e','h')
  .join('')  // new String('olleh')
```

> When I want to reverse the string I turn it into an array 'cause Arrays are 
  good for iterating over stuff and being ordere. Strings know how to become 
  arrays know how to become strings.


```js
console.log(
  reverse(new String('{^%34')) // => '43%^{'
)
```

> Generic data, reveresed! 


```js
const words = new Array(new String('hello'), new String('bye'))
```

> How do I reverse a bunch of words?


```js
const words = new Array(new String('hello'), new String('bye'))
const reversedWords = words.map(reverse)
```

> Actually, how do I transform the value of an array? use `.map`



## Intuition, revenge of.


```js
new Promise((resolve, reject) => resolve('hello'))
```

> What is this mysterious new structure? A promise you say? 



# TODO
  - Ask for values out of structures, do not take them `array.map` vs `array[0]`
