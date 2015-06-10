# Get Lifted
A Talk About JavaScript Promises

by [@legittalon][twitter]

[twitter]: https://twitter.com/legittalon

> I am Talon. Community Slack link on meetup page.



## *Question*: What is a Promise?

<span class="fragment">*Answer*: A structure.</span>

> Promises are *just* structures. 



# Intuition

> How do I represent generic text?


```js
const word = new String('hello')
```

> Strings are a structure that represent generic text.


```js
const reverse = string => string
  .split('') // new Array('h','e','l','l','o') 
  .reverse() // new Array('o','l','l','e','h')
  .join('')  // new String('olleh')
```

> When I want to reverse the string I turn it into an array 'cause Arrays are 
  good for iterating over stuff. Strings know how to become arrays know how to
  become strings.


```js
console.log(
  reverse(new String('{^%34')) // => '43%^'
)
```

> Strings can be really weird, but the function works as desired.


```js
const words = new Array(new String('hello'), new String('bye'))
```


```js
const words = new Array(new String('hello'), new String('bye'))
const reversedWords = words.map(reverse)
```



## Intuition, revenge of.


```js
new Promise((resolve, reject) => resolve('hello'))
```

> Array's are structures
