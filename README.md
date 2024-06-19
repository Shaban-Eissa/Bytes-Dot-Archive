# Bytes Dot Archive 📚✨

Welcome to **BytesDotArchive**! 🎉

This repository is a curated collection of coding quizzes from the [Bytes.dev](https://bytes.dev/) newsletter archives. Bytes.dev is a fantastic resource for web developers, offering the latest news, tutorials, and tips. Each issue includes a fun and challenging quiz section that helps developers sharpen their skills and stay engaged with the latest trends and practices in the industry.

## About the Collection 🗂️

### What's Inside:
- **Quizzes from each newsletter issue**: Arranged by issue number.
- **Various coding challenges**: Includes JavaScript puzzles and debugging exercises.

## How to Use 🛠️

Explore the quizzes, test your knowledge, and contribute by adding new quizzes or enhancing existing ones. This collection aims to foster learning and collaboration within the developer community.

## Contributions 🤝

We welcome your input! If you have suggestions, improvements, or new quizzes to add, please submit a pull request or open an issue. Let's build this resource together!


## Quizzes and Solutions

#### Issue 1 - Spot the Bug

```javascript
const Animal = (name, type) => {
  this.name = name
  this.type = type
  this.age = 0
}

Animal.prototype.birthday = function () {
  this.age++
}

const leo = new Animal('Leo', 'Lion')


// Arrow functions don’t have their own this. This leads to three errors in our code.

// First, we’re adding properties to this in the constructor function. Again, because Arrow Functions don’t have their own this, you can’t do that.

// Second, we can’t use the new keyword with an Arrow Function. This will throw a X is not a constructor error.

// Third, we can’t add a property on a function’s prototype if that function is an arrow function, again, because there’s no this.

```

#### Spot the Bug - Answer

```js
function Animal (name, type) {
  this.name = name
  this.type = type
  this.age = 0
}

Animal.prototype.birthday = function () {
  this.age++
}

const leo = new Animal('Leo', 'Lion')
```
<br />
<hr />

#### Issue 2 - Spot the Bug

```js
function Animal (name, type) {
  this.name = name
  this.type = type
  this.age = 0
}

Animal.prototype.birthday = function () {
  this.age++
}

const leo = Animal('Leo', 'Lion')
```

#### Spot the Bug - Answer
```js
function Animal (name, type) {
  this.name = name
  this.type = type
  this.age = 0
}

Animal.prototype.birthday = function () {
  this.age++
}

const leo = new Animal('Leo', 'Lion')
```
Inside our Animal constructor function, we’re relying on JavaScript to create a this object for us. However, in order for it to know to do that, we need to invoke the function with the new keyword.


<br />
<hr />

#### Issue 4 - Spot the Bug

```js
function calcPrice (price, tax, discount) {
  tax = tax || 0.05
  discount = discount || 0

  return // math
}

calcPrice(10, 0, .1)
```

#### Spot the Bug - Answer
The || operator checks for falsy values and 0 is a falsy value. To fix this, instead of checking for a falsy value, you can check for undefined or just use ES6’s Default Parameters.

Spot the Bug - Solution(s)
```js
// es5
function calcPrice (price, tax, discount) {
  tax = typeof tax === 'undefined'
    ? 0.05
    : tax
  discount = typeof discount === 'undefined'
    ? 0
    : discount

  return // math
}
```

or using ES6’s default parameters
```js
function calcPrice (price, tax = 0.05, discount = 0) {
  return // math
}
```

<br />
<hr />

#### Issue 5 - How many times is the reducer function invoked?

```js
const nums = [2,4,6]

const reducer = (prev, current) => {
  console.count('invoked')
  return prev + current
}

nums.reduce(reducer)
```

#### Answer: Twice

If an initial value isn’t supplied, the first element in the array will be used as the initial value and the first invocation of the reducer function will be skipped.


<br />
<hr />

#### Issue 10 - Spot the Bug

```js
function Animal (name, energy) {
  let animal = {}
  animal.name = name
  animal.energy = energy

  return animal
}

Animal.prototype.eat = function (amount) {
  console.log(`${this.name} is eating.`)
  this.energy += amount
}

const leo = Animal('Leo', 7)
leo.eat(5)
```

#### Spot the Bug - Answer
Our call to leo.eat is going to fail. The reason for this is because the object returned from Animal isn’t delegating to Animal.prototype so leo.eat will be undefined.

To fix this, we can use Object.create or a combination of the this keyword with new.

```js
function Animal (name, energy) {
  let animal = Object.create(Animal.prototype)
  animal.name = name
  animal.energy = energy

  return animal
}

// or

function Animal (name, energy) {
  this.name = name
  this.energy = energy
}

const leo = new Animal('Leo', 7)
```
For more details, check out [A Beginner’s Guide to JavaScript’s Prototype](https://ui.dev/beginners-guide-to-javascript-prototype).


<br />
<hr />

#### Issue 11 - What will be logged to the console after the code is finished executing?

```js
function first () {
  var name = 'Jordyn'

  console.log(name)
}

function second () {
  var name = 'Jake'

  console.log(name)
}

console.log(name)
var name = 'Tyler'
first()
second()
console.log(name)
```

#### Answer

We get undefined, Jordyn, Jake, then Tyler. What this shows us is that you can think of each new Execution Context as having its own unique variable environment. Even though there are other Execution Contexts that contain the variable name, the JavaScript engine will first look to the current Execution Context for that variable.

For more info and to see [a cool GIF](https://ui.dev/post-images/unique-scopes.gif) on how the JS interpreter evaluates the code above, visit [The Ultimate Guide to Hoisting, Scopes, and Closures in JavaScript](https://ui.dev/ultimate-guide-to-execution-contexts-hoisting-scopes-and-closures-in-javascript)


<br />
<hr />

#### Issue 12 - Spot the Bug

```js
function capitalize (string) {
  string[0].toUpperCase()
  return string
}
```

#### Spot the Bug - Answer

When we call toUpperCase, we’re assuming that we’re modifying the string that was passed into the function. However, since strings are primitive values, that means they’re immutable and can’t be modified once they’re been created. Instead of trying to modify the string directly, we need to return a new string after capitalizing the first character.

```js
const capitalize = ([firstLetter, ...restOfWord]) => {
  return firstLetter.toUpperCase() + restOfWord.join('')
}
console.log(capitalize('hello')) // Hello
```
For more information, visit [How to capitalize the first letter of a string in JavaScript](https://ui.dev/capitalize-first-letter-of-string-javascript)


<br />
<hr />

#### Issue 13 - Get the current URL in JavaScript

```js
function getCurrentURL () {
  return window.location.href
}

// Example
const url = getCurrentURL()

url // https://ui.dev/get-current-url-javascript/
```

Simple enough. If you’re using JavaScript in the browser you can get the full current URL by using window.location.href. I think it’s also worth noting that window.location has a bunch of different properties on it that may be of use to you as well.

Let’s assume this is the current URL we’re on

```js
https://ui.dev/get-current-url-javascript/?comments=false
```
These are all the properties that window.location gives us.

```js
const {
  host, hostname, href, origin, pathname, port, protocol, search
} = window.location

host // "ui.dev"
hostname // "ui"
href // "https://ui.dev/get-current-url-javascript/?comments=false"
origin // "https://ui.dev"
pathname // "/get-current-url-javascript/""
port // ""
protocol // "https:"
search // "?comments=false"
```

<br />
<hr />

#### Issue 14 - In what order will the logs below show up in the console?

```js
console.log('First')

setTimeout(function () {
  console.log('Second')
}, 0)

new Promise(function (res) {
  res('Third')
}).then(console.log)

console.log('Fourth')
```

#### Answer 
First, Fourth, Third, Second.

To fully understand this one you need an understanding of JavaScript’s event loop, specifically, the Call Stack, Task Queue, Web APIs (for setTimeout), and the Job Queue.

<br />
<hr />

#### Issue 15 - Why does this code work?

```js
const friends = ['Alex', 'AB', 'Mikenzi']
friends.hasOwnProperty('push') // false
```
Specifically, why does friends.hasOwnProperty('push') work even though friends doesn’t have a hasOwnProperty property and neither does Array.prototype?

#### Answer 

As mentioned earlier, if you look at Array.prototype, it doesn’t have a hasOwnProperty method. How then, does the friends array have access to hasOwnProperty?

The reason is because the Array class extends the Object class. So when the JavaScript interpreter sees that friends doesn’t have a hasOwnProperty property, it checks if Array.prototype does. When Array.prototype doesn’t, it checks if Object.prototype does, it does, then it invokes it.

```js
const friends = ['Alex', 'AB', 'Mikenzi']

console.log(Object.prototype)
/*
   constructor: ƒ Object()
   hasOwnProperty: ƒ hasOwnProperty()
   isPrototypeOf: ƒ isPrototypeOf()
   propertyIsEnumerable: ƒ propertyIsEnumerable()
   toLocaleString: ƒ toLocaleString()
   toString: ƒ toString()
   valueOf: ƒ valueOf()
*/

friends instanceof Array // true
friends instanceof Object // true

friends.hasOwnProperty('push') // false
```

<br />
<hr />

#### Issue 17 - Spot the Bug

```js
const Animal = (name, type) => {
  this.name = name
  this.type = type
  this.age = 0
}

Animal.prototype.birthday = function () {
  this.age++
}

const leo = new Animal('Leo', 'Lion')
```


#### Spot the Bug - Answer
Arrow functions don’t have their own this. This leads to three errors in our code.

First, we’re adding properties to this in the constructor function. Again, because Arrow Functions don’t have their own this, you can’t do that.

Second, we can’t use the new keyword with an Arrow Function. This will throw a X is not a constructor error.

Third, we can’t add a property on a function’s prototype if that function is an arrow function, again, because there’s no this.

```js
function Animal (name, type) {
  this.name = name
  this.type = type
  this.age = 0
}

Animal.prototype.birthday = function () {
  this.age++
}

const leo = new Animal('Leo', 'Lion')
```

<br />
<hr />

#### Issue 21 - 🔥 JS Tip

You can remove all “falsy” values from an Array by filtering for Boolean.

```js
const friends = [
  'Jake',
  null,
  'Cassidy',
  undefined,
  'Joshy',
  undefined,
  'Jordyn'
]

const filteredFriends = friends.filter(Boolean)
filteredFriends // ["Jake", "Cassidy", "Joshy", "Jordyn"]
```

<br />
<hr />

#### Issue 23 - 🔥 JS Tip - .find

One array method that I find is underrated is .find. It allows you to find the first element in an array which satisfies a test specified by a given function.

```js
const tweets = [
  { id: 1, stars: 13, text: 'Turns out "git reset --hard HEAD^" was a terrible idea.' },
  { id: 2, stars: 87, text: 'Tech conferences are too expensive.' },
  { id: 3, stars: 51, text: 'Clean code is subjective. Optimize for deletion.' },
  { id: 4, stars: 19, text: 'Maybe the real benefit of open source was the friendships we made along the way?' },
]

const tweet = tweets.find((t) => t.id === 3)

console.log(tweet) // {id: 3, stars: 51, text: "Clean code is subjective. Optimize for deletion."}
```

<br />
<hr />

#### Issue 24 - 🔥 JS Tip - .reduce

.reduce holds the keys to the universe. If you master it, you’ll be able to do pretty much anything you want with arrays. Before you even look at the API, it’s important to understand why .reduce exists. The idea of .reduce is that you can take an array and transform it into anything else - another array, an object, an integer, literally anything. Why would you ever want to do that? Look at every single example on this whole page. In each one, we’re taking an array and transforming it in some way - mostly to another array. Let’s look at some other common ways you’d transform an array.

```js
[1,2,3] -> sum-> 6

---

[
 { name: 'Tyler', age: 28},
 { name: 'Mikenzi', age: 26},
 { name: 'Blaine', age: 30 }
] -> Just the names -> ['Tyler', 'Mikenzi', 'Blaine']

---

[
 { name: 'Tyler', age: 28},
 { name: 'Mikenzi', age: 26},
 { name: 'Blaine', age: 30 }
] -> Length and age count -> { users: 3, ageTotal: 84}

---

[
  { id: 1, stars: 13, text: 'Turns out "git reset --hard HEAD^" was a terrible idea.' },
  { id: 2, stars: 87, text: 'Tech conferences are too expensive.' },
  { id: 3, stars: 51, text: 'Clean code is subjective. Optimize for deletion.' },
  { id: 4, stars: 19, text: 'Maybe the real benefit of open source was the friendships we made along the way?' },
]
  -> Remove the stars property ->
[
  { id: 1, text: 'Turns out "git reset --hard HEAD^" was a terrible idea.' },
  { id: 2, text: 'Tech conferences are too expensive.' },
  { id: 3, text: 'Clean code is subjective. Optimize for deletion.' },
  { id: 4, text: 'Maybe the real benefit of open source was the friendships we made along the way?' },
]
```

Here’s how I think about whether I should use .reduce or not.
1) Am I transforming an array into another array
just by removing some elements? Use .filter

2) Am I transforming an array into another array? Use .map

3) Am I transforming an array into something other than another array? Use .reduce

Now that we understand what .reduce is used for, let’s take a look at the API. Don’t worry if this is confusing, with great power comes great initial confusion. Google “reduce JavaScript” and read the first two pages of results. It’ll be worth it - promise.

I’ll first show you how to accomplish our goal of summing up an array of number into a single integer, then we’ll walk through it.

```js
function sum (arr) {
  return arr.reduce((total, num) => {
    return total + num
  }, 0)
}

sum([1,2,3]) // 6
sum([5,5,5]) // 15
```

Remember, the goal here is to take the array that’s being passed into the sum function and transform it into a single integer, which is the summation of all the numbers in the array.

The first thing you’ll notice is that we pass .reduce two arguments. The first is a function that will be invoked for every element in the array. The second is what we’ll call the “initial value”. In our example, because we’re adding all the numbers together, we want the initial value to be 0 (so we don’t run into any NaN problems). If we were creating a new object, the initial value would be an empty object. If we were creating an array, it would be an empty array.

Next, we need to figure out what the parameters are for the function we pass to .reduce. In our example, we named them total and num. Remember, this function is going to be called for each element in the array. The reason we named it num is because we’re reducing over an array full of integers and for each iteration, num is going to be whatever the number is in the array. We can see this in the example below.

```js
function sum (arr) {
  return arr.reduce((total, num) => {
    console.log(num)
  }, 0)
}

sum([1,2,3])
// 1
// 2
// 3
```

That makes sense. The next thing we need to figure out is total. This is where it gets a little mind-bendy. In our example, total is going to initially be 0, since that’s what we set our initial value to. After that, total is going to be whatever the previous iteration returned. We can see this clearly in the example below.

```js
function sum (arr) {
  return arr.reduce((total, num) => {
    console.log(total)
    return Date.now()
  }, 0)
}

sum([1,2,3])
```

The first time our callback function runs, it logs 0 to the console. Again, that’s because we set the initial value to 0. Then, for each new time the function runs, we get a timestamp in the console because that’s what we’re returning.

Now let’s take this knowledge and look back at our initial solution.

```js
function sum (arr) {
  return arr.reduce((total, num) => {
    return total + num
  }, 0)
}

sum([1,2,3])
```

The very first time the callback function runs, total will be 0 and num will be 1. Then, the next iteration, total will be 1 and num will be 2. The reason total is one is because we previously returned 0 + 1. Then, total will be 3 and num will be 3. Then, there are no more elements in the array so what gets returned is 6. We can see this in the diagram below.

```js
Initial Value: 0

First iteration:
  total: 0
  num: 1

Second iteration:
  total: 1
  num: 2

Third iteration:
  total: 3
  num: 3

No more elements in the array, return 3 + 3 which is 6.
```

Let’s look at the example where we convert an array of objects into another object.

```js
[
 { name: 'Tyler', age: 28},
 { name: 'Mikenzi', age: 26},
 { name: 'Blaine', age: 30 }
] -> Length and age count -> { users: 3, ageTotal: 84}
```

First, what do we want the initial value to be? We want it to be an object with a users property as well as an ageTotal property, both set to 0.

```js
function getUserData (users) {
  return users.reduce(() => {

  }, { users: 0, ageTotal: 0 })
}
```

Now we need to figure out what each iteration looks like. We know what we want to return is the initial object, adding 1 to the users property and adding whatever the user’s age is to the ageTotal property.

```js
function getUserData (users) {
  return users.reduce((data, user) => {
    data.users += 1
    data.ageTotal += user.age

    return data
  }, { users: 0, ageTotal: 0 })
}

const users = [
 { name: 'Tyler', age: 28},
 { name: 'Mikenzi', age: 26},
 { name: 'Blaine', age: 30 }
]

getUserData(users) // { users: 3, ageTotal: 84 }
```

Impressive, yeah? Odds are this is still a bit fuzzy. The best thing you can do is take an array, and practice transforming it into anything you can think of.

<br />
<hr />

#### Issue 26 - 🔥 JS Tip - Format Numbers to Dollars in JS

```js
function formatToDollar (number) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
  }).format(number)
}

formatToDollar(873) // "$873.00"
formatToDollar(1634) // "$1,634.00"
formatToDollar(1523.65) // "$1,523.65"
formatToDollar(1893042.3498) // "$1,893,042.35"
```

In the example above we see how you can use the Intl.NumberFormat API to format numbers as dollars in JavaScript. Let’s walk through the different options in case you need to customize it for yourself.

style is the formatting style to use. There are three options - decimal (default), currency, and percent.

If you’re using a style of currency as we are above, you also need to specify the currency format, in our case, USD. Other options include EUR for the Euro, CNY for the Chinese RMB, MXN for the Peso, or any other “ISO 4217” currency.

If you need more fine tuned customization, you can view the [full API here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat#Parameters).


<br />
<hr />

#### Issue 30 - 🔥 JS Tip - Loops and Labels

JavaScript has at least 20 different ways to loop over things, including all of the array methods, like forEach, map, and filter; recursive functions; and while, and for.

For array methods and recursive functions, you can end a loop early with a return statement, but if you were to use a return statement in a while or for loop, it would end the entire function, which is not ideal. Instead, if you want to jump to the next iteration of the loop, you can use the continue statement, like so.

```js
for (let i = 0; i < 10; i++) {
  // Skip multiples of 2
  if (i % 2 === 0) {
    continue
  }
  console.log(i)
}
// 1, 3, 5, 7, 9
```
The break statement lets you end the loop prematurely, without running any more iterations.

```js
for (let i = 0; i < 10; i++) {
  // End the loop when we get to a multiple of 3
  if (i % 3 === 0) {
    break
  }
  console.log(i)
}
// 1, 2
```

These two statements work great for individual loops, but what if we needed to coordinate nested loops? If we just used break or continue inside the inner loop, it wouldn’t be able to stop or skip the outer loop.

```js
const numberList = [1, 2, 3, 4, 5]
for (let i = 0; i < numberList.length; i++) {
  const iNum = numberList[i]
  for (let j = 0; j < numberList.length; j++) {
    const jNum = numberList[j]
    if ((iNum * jNum) % 2 === 0) {
      // This continues the inner loop if the number is even
      continue
    }
    console.log(iNum * jNum)
  }
}
// 1,3,5,3,9,15,5,15,25
```

To let us call continue or break on the outer loop from inside the inner loop, we need to apply a label to the outer loop. The label goes right before the for statement. Then, we can use the label with the continue statement. Notice how the results change once we add the label.

```js
const numberList = [1, 2, 3, 4, 5]
outerLoop: for (let i = 0; i < numberList.length; i++) {
  const iNum = numberList[i]
  for (let j = 0; j < numberList.length; j++) {
    const jNum = numberList[j]
    if ((iNum * jNum) % 2 === 0) {
      // This continues the inner loop if the number is even
      continue outerLoop
    }
    console.log(iNum * jNum)
  }
}
// 1,3,5
```
Next time you need to nest loops for some reason, you can use a label, break, and continue to have more control over the flow of your loops.



<br />
<hr />

#### Issue 30 - Spot the Bug

```js
function Animal (name, energy) {
  let animal = {}
  animal.name = name
  animal.energy = energy

  return animal
}

Animal.prototype.eat = function (amount) {
  console.log(`${this.name} is eating.`)
  this.energy += amount
}

const leo = Animal('Leo', 7)
leo.eat(5)
```

#### Spot the Bug - Answer
Our call to leo.eat is going to fail. The reason for this is because the object returned from Animal isn’t delegating to Animal.prototype so leo.eat will be undefined.

To fix this, we can use Object.create or a combination of the this keyword with new.

```js
function Animal (name, energy) {
  let animal = Object.create(Animal.prototype)
  animal.name = name
  animal.energy = energy

  return animal
}

// or

function Animal (name, energy) {
  this.name = name
  this.energy = energy
}

const leo = new Animal('Leo', 7)
```

For more details, check out [A Beginner’s Guide to JavaScript’s Prototype](https://ui.dev/beginners-guide-to-javascript-prototype).


<br />
<hr />

#### Issue 36 - 🔥 JS Tip 

If you’re like me, you use one of these strategies for logging a value to the console.

```js
const name = 'Tyler'

console.log('name', name) // name Tyler
console.log('HERE', name) // HERE Tyler
console.log('sefkjse', name) // sefkjse Tyler
console.log('wakawaka', name) // wakawaka Tyler
```

Believe it or not, there’s a better way and it utilizes object destructuring.

```js
const name = 'Tyler'

console.log({ name }) // {name: 'Tyler'}
```

<br />
<hr />


#### Issue 37 - 🔥 JS Tip 

Sometimes you want to remove a property/value from an object. Using the power of JavaScript™ (and ES6’s rest operator), you can do it like this.

```js
const user = {
  name: 'Tyler',
  age: 30,
  date: 1614619969641,
  funny: true
}

const { funny, ...updatedUser } = user

console.log(updatedUser) // {name: "Tyler", age: 30, date: 1614619969641}
```



<br />
<hr />


#### Issue 51 - 🔥 JS Tip 

Sometimes (mostly in job interviews) you need to write a function to find the longest word in a string. Here’s one implementation using .reduce that’ll do it.

Is it the best? I don’t know, but I dig it.

```js
function findLongestWord (str) {
  return str.split(' ')
    .reduce((longest, word) =>
      word.length > longest.length 
        ? word 
        : longest
  , '')
}

findLongestWord('Find the longest word') // longest
```
Note it’ll return the first word if there’s a tie. If you’re in a job interview, that’s a good question to clarify before diving into the code.


<br />
<hr />


#### Issue 53 - 🔥 JS Tip 

Want to use console.log without breaking apart your one line arrow function? Use the || operator.

```js
export default connect (
  ({planeteers}) => console.log(planeteers) || ({capPlanet: planeteers.captain})
)
```


<br />
<hr />


#### Issue 71 - Spot the Bug

```js
const petName = 'Leo'
const placeholder = '{NAME}'
const reminderTemplate = '{NAME} is due for another visit. Please call us so we can set up a new appointment. We look forward to seeing you and {NAME} soon.'

const reminder = reminderTemplate.replace(placeholder, petName)
```

#### Spot the Bug - Answer
String.prototype.replace only replaces the first occurrence found in the string. If there could be more than one occurrence, use String.prototype.replaceAll which is part of ES2021.

```js
const petName = 'Leo'
const placeholder = '{NAME}'
const reminderTemplate = '{NAME} is due for another visit. Please call us so we can set up a new appointment. We look forward to seeing you and {NAME} soon.'

const reminder = reminderTemplate.replaceAll(placeholder, petName)
```


<br />
<hr />


#### Issue 72 - JS Quiz

What will be logged to the console when this code executes? The answer is below.

```js
window.name = "Mike Tyson";

const me = {
  name: "Tyler",
  sayName() {
    console.log(this.name);
  },
};

const sayName = me.sayName;
sayName();
```

#### JS Quiz - Answer
The answer? “Mike Tyson”.

Since we’re not in strict mode, sayName isn’t a method, and we’re not using call or apply, this inside of sayName will default to the window object.

<br />
<hr />


#### Issue 91 - Spot the Bug

```js
function addAndSort(array, element) {
  return array.push(element).sort();
}
```

#### Spot the Bug - Solution

When you call array.push on an array, it doesn’t return the updated array, but rather the length of the array with the new item. That means you can’t chain the .sort() call to the end, since the result of .push is a number.

There are two ways to fix this. One option is to call array.sort() after the .push call.

```js
function addAndSort(array, element) {
  array.push(element)
  return array.sort();
}
```

The second option appends the item to a new array with array.concat() and then sorts the new array.

```js
function addAndSort(array, element) {
  return array.concat(element).sort();
}
```


<br />
<hr />


#### Issue 96 - Spot the Bug

```js
function todoReducer(state, action) {
  switch (action.type) {
    case "ADD_TODO":
      const todos = state.todos;
      return { ...state, todos: todos.concat(action.payload) };
    case "REMOVE_TODO":
      const todos = state.todos;
      const newTodos = todos.filter(todo => todo.id !== action.id);
      return { ...state, todos: newTodos };
    default:
      return state;
  }
}
```

#### Spot the Bug - Solution

The todos variable is being re-declared within the same block. Variables declared with const and let are block-scoped, meaning they don’t exist outside of the block they were called in. Blocks are created with {} brackets around if/else statements, loops, and functions.

There are many solutions, including changing the variable name in the different cases or removing the variable altogether. We can also wrap each of our cases in a block to isolate the variables.

```js
function todoReducer(state, action) {
  switch (action.type) {
    case "ADD_TODO": {
      const todos = state.todos;
      return { ...state, todos: todos.concat(action.payload) };
    }
    case "REMOVE_TODO": {
      const todos = state.todos;
      const newTodos = todos.filter((todo) => todo.id !== action.id);
      return { ...state, todos: newTodos };
    }
    default:
      return state;
  }
}
```


<br />
<hr />


#### Issue 100 - Spot the Bug

```js
function factorial(n) {
  let result = 1;
  for (const i = 1; i < n + 1; i++) {
    result *= i; 
  }
  return result;
}
```

#### Spot the Bug - Solution

For loops work by assigning a value to the variable for each iteration, but variables defined with const can’t be reassigned. Instead, we should use let to define our variable.

```js
function factorial(n) {
  let result = 1;
  for (let i = 1; i < n + 1; i++) {
    result *= i; 
  }
  return result;
}
```

<br />
<hr />


#### Issue 104 - JS Quiz 

```js
const friends = ['Aliyah', 'Alex', 'Ben', 'Cassidy', 'Carlos']

const { length, 0: first, [length - 1]: last } = friends

console.log(first) 
console.log(last) 
```

#### JS Quiz Solution 

```jsconst friends = ['Aliyah', 'Alex', 'Ben', 'Cassidy', 'Carlos']

const { length, 0: first, [length - 1]: last } = friends

console.log(first) // Aliyah
console.log(last) // Carlos
```

Since arrays are just objects with numeric keys and a length property, we can use destructuring and computed property names in order to grab the first and last elements in any array. Kind of worthless, but kind of cool.

<br />
<hr />


#### Issue 105 - JS Quiz - What gets logged?

```js
function Dog(name) {
  this.name = name
  this.speak = () => 'Woof Woof'
}

Dog.prototype.speak = function() {
  return 'Ruff Ruff'
}

const dog = new Dog('Leo')
console.log(dog.speak())
```

#### JS Quiz Solution 

Woof Woof gets logged.

Before JavaScript delegates the lookup of the property to the Constructor’s prototype, it first checks to see if the property exists on the object being returned from the Constructor. In this case, it does so it calls it.


<br />
<hr />


#### Issue 111 - JS Tip

How can we improve this code?
```js
async function completeCheckout(orderId) {
  await updateAnalytics(orderId);
  const order = await processOrder(orderId);

  return order;
}
```

####  Solution 

Because processOrder doesn’t depend on the result of updateAnalytics, we can parallelize the two invocations.

```js
async function completeCheckout(orderId) {
  const [_, order] = await Promise.all([
    updateAnalytics(orderId),
    processOrder(orderId)
  ])

  return order;
}
```


<br />
<hr />


#### Issue 112 - JS Quiz

What order will this code log?
```js
const arr = [7, 1, 4, 3, 2];

for (const elem of arr) {
  setTimeout(() => console.log(elem), elem);
}
```

####  Solution 

If you chose [7, 1, 4, 3, 2] because of how most run-times used to handle clamping, you are probably very smart and in this scenario, very wrong.

The answer is [1, 2, 3, 4, 7] – or as I like to call it, a really bad way to pass a sorting algorithm technical interview.


<br />
<hr />


#### Issue 120 - SPOT THE BUG

```js
const getCapitalizedInitials = (name) =>
  name
    .trim()
    .split(" ")
    .forEach((name) => name.charAt(0))
    .join("")
    .toUpperCase()
```

####  SPOT THE BUG: SOLUTION

We’re treating forEach as if it returned an array, when it actually returns undefined. Instead, we want to use map, which works similar to forEach, but also creates and returns a new array.

```js
const getCapitalizedInitials = (name) =>
  name
    .trim()
    .split(" ")
    .map((name) => name.charAt(0))
    .join("")
    .toUpperCase()
```    

<br />
<hr />


#### Issue 122 - SPOT THE BUG

```js
const newsletter = "Bytes"
const tagline = "Your weekly dose of JavaScript"

[newsletter, tagline].forEach((el) => console.log(el))
```

####  SPOT THE BUG: SOLUTION

You might be surprised to learn that this code doesn’t execute. If you try, you’ll get an error – Uncaught ReferenceError: tagline is not defined. But clearly it is, right? Wrongo.

This is the very rare scenario where not using semicolons can bite you. Because we have a string followed by no semicolon followed by an opening array bracket, JavaScript interprets our code like this, as if we’re trying to access elements from the string.

```js
"Your weekly dose of JavaScript"[newsletter, tagline].forEach();
```

This, of course, throws an error because tagline isn’t defined. To fix this, add a + sign before the array.

```js
const newsletter = "Bytes"
const tagline = "Your weekly dose of JavaScript"

+[newsletter, tagline].forEach((el) => console.log(el))
```

That’s mostly a joke, but it does work…

Instead, just use semicolons.

```js
const newsletter = "Bytes";
const tagline = "Your weekly dose of JavaScript";

[newsletter, tagline].forEach((el) => console.log(el));
```



<br />
<hr />


#### Issue 124 - SPOT THE BUG

```js
const user = {
  name: 'Tyler',
  age: 32,
  greet() {
    alert(`Hello, my name is ${this.name}`)
  },
  mother: {
    name: 'Jan',
    greet() {
      alert(`Hello, my name is ${this.mother.name}`)
    }
  }
}

user.mother.greet()
```

####  SPOT THE BUG: SOLUTION

When we invoke user.mother.greet, we can tell what the this keyword is referencing by looking to the “left of the dot” of the invocation – in this case, mother.

So inside of greet, it’s as if we had my name is ${mother.mother.name}, which is clearly wrong. Instead, since the this keyword is referencing mother, we can just do this.name.

```js
const user = {
  name: 'Tyler',
  age: 32,
  greet() {
    alert(`Hello, my name is ${this.name}`)
  },
  mother: {
    name: 'Jan',
    greet() {
      alert(`Hello, my name is ${this.name}`)
    }
  }
}

user.mother.greet()
```


<br />
<hr />


#### Issue 138 - POP QUIZ - What gets logged?

```js
let i = 0

function x() {
  i++
  return 10
}

i += x()

console.log(i) // ?
```

####  POP QUIZ: ANSWER
The answer is 10. Here’s how it works.

For clarity, we can refactor i += x() to be i = i + x(). From there, the interpreter begins evaluating our code. Before it evaluates the function invocation, it seems that i evaluates to 0, so now our code is i = 0 + x(). The invocation of x returns 10, so now it’s i = 0 + 10, which gives us i = 10.

Note that if you swap the order of i and x() like i = x() + i you get a different value.



<br />
<hr />


#### Issue 142 - POP QUIZ - What gets logged?

```js
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 1000)
}
```

####  POP QUIZ: ANSWER

This code will log 5 5 times.

The reason for this is because we declared our variable with var, which is function scoped. By the time our functions given to setTimeout run, i will already be 5 and every function will reference that same variable. To fix this, use let which is block scoped and will give each iteration of our for loop its own i.

```js
for (let i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 1000)
}
```



<br />
<hr />


#### Issue 144 - SPOT THE BUG

```js
function getEvenNumbers(numbers) {
  let evenNumbers = [];

  for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] % 2 === 1) {
      evenNumbers.push(numbers[i]);
    }
  }

  return evenNumbers;
}

getEvenNumbers([1,2,3,4,5,6])
```

####  SPOT THE BUG: SOLUTION

Our logic is a little off. n % 2 will return 0 if n is an even number. The bug is that our code checks if it returns 1 (which would be an odd number).

To fix this, we can change that line to see if it evaluates to 0, not 1.

```js
function getEvenNumbers(numbers) {
  let evenNumbers = [];

  for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] % 2 === 0) {
      evenNumbers.push(numbers[i]);
    }
  }

  return evenNumbers;
}

getEvenNumbers([1,2,3,4,5,6])
```


<br />
<hr />


#### Issue 151 - How can this code be improved?

```js
fetch("/user")
  .then((res) => res.json())
  .then((user) => {

  })
```

#### SOLUTION

As is, if our server responds with anything other than the user (like a 400, 404, 500, etc.), we don’t handle those scenarios. You might think we can just add on a catch.

```js
fetch("/user")
  .then((res) => res.json())
  .then((user) => {

  })
  .catch((err) => {

  })
```

Not quite. The problem is catch isn’t triggered for any of those status codes. And worse, even if you wanted to check for the status of the request, you already ignored it when you converted the response to JSON in the first .then.

The better approach is something like this, where you check the status before converting to JSON.

```js
fetch("/user")
  .then((res) => {
    if (!res.ok) {
      // Check the status
      // to decide what you do
    }

    return res.json()
  })
  .then((user) => {

  })
  .catch((err) => {

  })
```


<br />
<hr />


#### Issue 154 - POP QUIZ
How would you remove the duplicate elements from this array?

```js
const list = [
  { name: 'John' }, 
  { name: 'Sara' },
  { name: 'Sara' },
  { name: 'Lynn' },
  { name: 'Jake' }
];
```

#### POP QUIZ: ANSWER

There are a few ways to do this. Your first intuition might be to do something like this.

```js
const uniqueList = Array.from(new Set(list))
```
It’s the right idea since creating a Set will ensure our collection only contains unique values and Array.from allows us to create a new, shallow-copied array. Unfortunately, Sets only enforce uniqueness for primitive values, but our list is full of objects.

Instead, we can do something like this.

```js
const list = [
  { name: 'John' }, 
  { name: 'Sara' },
  { name: 'Sara' },
  { name: 'Lynn' },
  { name: 'Jake' }
];

const map = new Map();

list.forEach(item => {
	map.set(item.name, item)
});

const uniqueList = Array.from(map.values())
```

Notice we’re using a Map here. Since Map’s preserve insertion order, our uniqueList will have the same order as the original list, but without the duplicates since we’re using name as the key.



<br />
<hr />


#### Issue 155 - POP QUIZ
What does this function do?

```js
const surprise = (...fns) => input => fns.reduce(
  (acc, fn) => fn(acc), input
)
```

#### POP QUIZ: ANSWER
It’s a pipe function that allows you to chain multiple operations together by taking a series of functions as arguments and applying them in a specific order to the input.

Wow, words.

Instead of doing something like this.

```js

const toUpperCase = str => str.toUpperCase()
const removeSpaces = str => str.replace(/\s/g, "")
const addExclamation = str => str + "!"

toUpperCase(removeSpaces(addExclamation("Subscribe to Bytes")))
```

You can do something like this.

```js
const pipe = (...fns) => input => fns.reduce(
  (acc, fn) => fn(acc), input
)

const formatString = pipe(toUpperCase, removeSpaces, addExclamation)

formatString("Subscribe to Bytes") // SUBSCRIBETOBYTES!
```



<br />
<hr />


#### Issue 163 - POP QUIZ
In the code snippet below, what do a and b evaluate to?

```js
let sum = 0;
const squares = [1, 2, 3, 4, 5].map((x) => (
  (sum += x), x * x
));

console.log(sum) // ?
console.log(squares) // ?
```

#### POP QUIZ: ANSWER

```js
let sum = 0;
const squares = [1, 2, 3, 4, 5].map((x) => (
  (sum += x), x * x
));

console.log(sum) // 15
console.log(squares) // [1, 4, 9, 16, 25]
```

This is a fun one. The weirdest part is probably the comma , operator.

If you’re not familiar, , evaluates each of its operands (from left to right) and returns the value of the last operand. This allows us to, in a single line, increase sum by x and return the square of x. When finished, we get the sum of the array as well as a new array of squares.

<br />
<hr />

#### Issue 164 - THE TIP
How would you add a console.log to this expression?

```js
const names = ["Ben", "Alex", "Lynn", "Tyler"];
const mappedNames = names.map(name => ({ 
  name, 
  company: "uidotdev"
}));
```

#### ANSWER

You could rewrite the function to use a block body, but ain’t nobody got time for that. Because console.log returns undefined we can use the logical OR operator (||) to add the log inline.

```js
const names = ["Ben", "Alex", "Lynn", "Tyler"];
const mappedNames = names.map(name => console.log(name) || ({ 
  name, 
  company: "uidotdev"
}));
```


<br />
<hr />

#### Issue 167 - POP QUIZ
Nested loops aren’t ideal, but sometimes they’re unavoidable. Given the nested loop below, how can we break out of the nested loop when j === 2?

```js
function loop () {
  for (let i = 0; i < 4; i++) {
    for (let j = 0; j < 4; j++) {
      if (j === 2) {
        // Break out here
      }
    }
  }
}
```

#### POP QUIZ: ANSWER

It’s rarely used, but in JavaScript you can use a labeled statement to add a label to a for loop. This then allows you to break and interrupt the loop when needed – even from inside another loop.

```js
function loop () {
  dance:
  for (let i = 0; i < 4; i++) {
    for (let j = 0; j < 4; j++) {
      if (j === 2) {
        break dance;
      }
    }
  }
}
```

<br />
<hr />

#### Issue 177 - SPOT THE BUG

```js
function deepCopy(obj) {
  return JSON.parse(JSON.stringify(obj));
}

const user = {
  name: 'Tyler',
  age: 32,
  created: new Date(),
}

const copiedUser = deepCopy(user)
```

#### SPOT THE BUG: SOLUTION

A deep copy of an object is a copy whose properties do no share the same references as those of the source object from which the copy was made. One approach for deep copying in JavaScript is using JSON.stringify and JSON.parse.

This kind of works in our case, but it will convert created to a string. To prevent that, you can use window.structuredClone instead (assuming browser support).

```js
function deepCopy(obj) {
  return window.structuredClone(obj)
}
```


<br />
<hr />

#### Issue 181 - SPOT THE BUG

```js
function calculateAverage(arr) {
  let sum = 0;
  let count = 0;

  for (let i = 0; i < arr.length; i++) {
    if (arr[i] && typeof arr[i] === "number") {
      sum += arr[i];
      count++;
    }
  }

  return sum / count;
}
```

#### SPOT THE BUG: SOLUTION

If we pass calculateAverage an array that contains a 0, because we’re filtering out falsy values (of which 0 is one), our calculation will be wrong.

To fix our function, we can get rid of our truthy check (arr[i]) and just verify the element is a number.

```js
function calculateAverage(arr) {
  let sum = 0;
  let count = 0;

  for (let i = 0; i < arr.length; i++) {
    if (typeof arr[i] === "number") {
      sum += arr[i];
      count++;
    }
  }

  return sum / count;
}
```

<br />
<hr />

#### Issue 182 - POP QUIZ
How can you set a timeout for a fetch request?


#### POP QUIZ: ANSWER

Since the fetch API does not have a built-in timeout option, you can use the AbortController and Promise.race() to implement a timeout. Using Promise.race is a nice trick because it allows you to abort a single request or multiple requests at the same time.

```js
const abortController = new AbortController();
const signal = abortController.signal;

const fetch1 = fetch("https://api.example.com/data-1", { signal });
const fetch2 = fetch("https://api.example.com/data-2", { signal });

const timeout = new Promise((_, reject) => {
  const timeoutId = setTimeout(() => {
    reject(new Error("Request timed out"));
    abortController.abort(); // Abort the fetch request
    clearTimeout(timeoutId); // clear the timeout
  }, 5000);
});

Promise.race([fetch1, fetch2, timeout])
  .then((response) => console.log(response))
  .catch((error) => console.error(error));
```

<br />
<hr />

#### Issue 186 - POP QUIZ
What gets logged?

```js
const myObject = {};

const key = Symbol('key');

myObject[key] = 'this is the value for the key';

console.log(myObject[Symbol('key')]);
console.log(JSON.stringify(myObject));
```

#### POP QUIZ: ANSWER

1. undefined - The Symbol constructor creates a unique value, so the Symbol used to set the value of myObject[key] is not the same as the Symbol used to get the value of myObject[key].

2. {} - JSON.stringify ignores Symbol properties when stringifying an object.

This is useful for creating private properties on objects that can’t be accessed or modified outside of the object.


<br />
<hr />

#### Issue 193 - SPOT THE BUG

```js
function removeElement(array, elementToRemove) {
  for (let i = 0; i < array.length; i++) {
    if (array[i] === elementToRemove) {
      array.splice(i, 1);
    }
  }
}

let myArray = [1, 2, 3, 2, 4];
removeElement(myArray, 2);
```

#### SPOT THE BUG: SOLUTION

This solution isn’t ideal since it doesn’t account for the fact that the array is being modified as it’s being iterated over. When the element at index 1 is removed, the element at index 2 is shifted to index 1.

There are a bunch of ways to make this better, all with varying tradeoffs. This is probably the best one, which uses JavaScript’s filter method to return a new array after filtering out the elementToRemove.

```js
function removeElement(array, elementToRemove) {
  return array.filter((element) => element !== elementToRemove);
}
```


<br />
<hr />

#### Issue 200 - POP QUIZ

What gets logged?

```js
let sharedVariable = "initial";

setTimeout(() => {
  sharedVariable = "updated by first timeout";
}, 500);

setTimeout(() => {
  if (sharedVariable === "initial") {
    console.log("Shared variable not yet updated");
  } else {
    console.log("Shared variable was already updated");
  }
}, 500);
```

#### POP QUIZ: ANSWER

In JavaScript, the execution order for setTimeout callbacks with identical delays aren’t deterministic. This means we aren’t guaranteed that the first timeout callback will execute first (which can be the cause of some nasty and difficult to reproduce bugs). In reality it’s almost always what you’d expect (“Shared variable was already updated”), but it’s best not to rely on that behavior.



<br />
<hr />

#### Issue 214 - SPOT THE BUG

```js
const people = [
  { firstName: "Aaron", lastName: "Smith" },
  { firstName: "Émile", lastName: "Zola" },
  { firstName: "Charlotte", lastName: "Brown" },
  { firstName: "Beyoncé", lastName: "Knowles" },
  { firstName: "Ólafur", lastName: "Arnalds" },
  { firstName: "David", lastName: "Jones" },
  { firstName: "Zoë", lastName: "Deschanel" },
];

function sortAlphabetically(arr) {
  return arr.sort((a, b) => {
    if (a.firstName < b.firstName) {
      return -1;
    }

    if (a.firstName > b.firstName) {
      return 1;
    }

    return 0;
  });
}

sortAlphabetically(people);
```

#### SPOT THE BUG: SOLUTION

By default, string comparison in JavaScript is not language-sensitive (meaning it doesn’t take into account language-specific rules or special characters like accents), which results in the sorted list not being in the correct order.

The solution is to leverage Intl.Collator which enables language-sensitive string comparison.

```js
function sortAlphabetically(arr) {
  const collator = new Intl.Collator("en", { sensitivity: "base" });
  return arr.sort((a, b) => collator.compare(a.firstName, b.firstName));
}
```


<br />
<hr />

#### Issue 217 - POP QUIZ

How can we improve this code?

```js
async function completeCheckout(orderId) {
  await updateAnalytics(orderId);
  const order = await processOrder(orderId);

  return order;
}
```

#### POP QUIZ: ANSWER

Because processOrder doesn’t depend on the result of updateAnalytics, we can parallelize the two invocations.

```js
async function completeCheckout(orderId) {
  const [_, order] = await Promise.all([
    updateAnalytics(orderId),
    processOrder(orderId)
  ])

  return order;
}
```


<br />
<hr />

#### Issue 229 - POP QUIZ

What does this evaluate to?

```js
Array.from({ length: 26 }, (x, i) => (i + 10).toString(36)).join(", ")
```

#### POP QUIZ: ANSWER

The English alphabet as a string – 

a, b, c, d, e, f, g, h, i, j, k, l, m, n, o, p, q, r, s, t, u, v, w, x, y, z


<br />
<hr />

#### Issue 231 - POP QUIZ

What gets logged?

```js
const array = new Array(3).fill([])
array[0].push("bytes")
console.log(array)
```

#### POP QUIZ: ANSWER

```js
const array = new Array(3).fill([])
array[0].push("bytes")
console.log(array) // [ ["bytes"], ["bytes"], ["bytes"] ]
```

The key to understanding this one is in knowing that arrays in JavaScript are reference values.

When you call .fill([]), what you’re really doing is “filling up” the array with three references to the same array. You can kind of think of it like this.

```js
const reference = []
const array = new Array(3).fill(reference)
```

Where now, array has three elements and they’re all referencing the same reference array. Therefore, if you add an item to any of the three elements, since they all point to the same array, it’s as if you’re adding an item to all of them.

To get the same functionality without the referential weirdness, you can use Array.from.

```js
const array = Array.from({ length: 3 }, () => []);
array[0].push("bytes");  // [ ["bytes"], [], [] ]
```



<br />
<hr />

#### Issue 249 - SPOT THE BUG

```js
function sumArgs() {
  let sum = 0;

  arguments.forEach((arg) => {
    sum += arg;
  });

  return sum;
}

const result = sumArgs(1, 2, 3, 4, 5);
```

#### SPOT THE BUG: SOLUTION

In JavaScript, arguments is not an array, it is an “array-like object” 😅. Because it’s an iterable, you can use a for loop to iterate over it, but if you want to use array methods like forEach, you need to convert it to an array first. There are a few different ways to do this.

```js
function sumArgs() {
  let sum = 0;

  for (let i = 0; i < arguments.length; i++) {
    sum += arguments[i];
  }

  return sum;
}

const result = sumArgs(1, 2, 3, 4, 5);
```

Or you can use the rest operator to get the arguments as an array:

```js
function sumArgs(...args) {
  let sum = 0;

  args.forEach((arg) => {
    sum += arg;
  });

  return sum;
}

const result = sumArgs(1, 2, 3, 4, 5);
```

Or you can use Array.from to convert the arguments to an array:

```js
function sumArgs() {
  let sum = 0;

  Array.from(arguments).forEach((arg) => {
    sum += arg;
  });

  return sum;
}

const result = sumArgs(1, 2, 3, 4, 5);
```


<br />
<hr />

#### Issue 256 - POP QUIZ

```js
function p1() {
  return new Promise((resolve, reject) => {
    setTimeout(() => reject("Error in p1"), 1000);
  }).catch((error) => {
    console.error(error);
  })
}

function p2() {
  return new Promise((resolve) => {
    setTimeout(() => resolve("p2 resolved"), 1000);
  });
}

function pAll() {
  Promise.all([p2(), p1()])
    .then((results) => {
      console.log("All data resolved:", results);
    })
    .catch((error) => {
      console.error("Error resolving data:", error);
    });
}

pAll();
```

#### POP QUIZ: ANSWER

First, Error in p1 is logged, then [ 'p2 resolved', undefined ] is logged. Since p1 catches the rejection, it doesn’t propagate to the Promise.all catch handler allowing p2 to resolve. But, since p1 doesn’t return anything, it’s result is undefined.


<br />
<hr />

#### Issue 263 - SPOT THE BUG

```js
let seats = [
  [1, 1, 0, 1, 0],
  [0, 1, 1, 1, 0],
  [1, 0, 1, 0, 0],
];

function reserveFirstAvailableSeat(seats) {
  for (let i = 0; i < seats.length; i++) {
    for (let j = 0; j < seats[i].length; j++) {
      if (seats[i][j] === 0) {
        seats[i][j] = 1; // Reserve the seat
        console.log(`Reserved seat at row ${i + 1}, column ${j + 1}`);
        break;
      }
    }
  }
}

reserveFirstAvailableSeat(seats);
```

#### SPOT THE BUG: SOLUTION

The code ends up making 3 reservations instead of 1. This is because the break statement only breaks out of the inner loop, not the outer loop. To fix this, you can replace the break statement with a return statement.

```js
let seats = [
  [1, 1, 0, 1, 0],
  [0, 1, 1, 1, 0],
  [1, 0, 1, 0, 0],
];

function reserveFirstAvailableSeat(seats) {
  for (let i = 0; i < seats.length; i++) {
    for (let j = 0; j < seats[i].length; j++) {
      if (seats[i][j] === 0) {
        seats[i][j] = 1; // Reserve the seat
        console.log(`Reserved seat at row ${i + 1}, column ${j + 1}`);
        return;
      }
    }
  }
}

reserveFirstAvailableSeat(seats);
```

Alternatively, you can use labeled statements to explicitly break out of the outer loop:

```js
let seats = [
  [1, 1, 0, 1, 0],
  [0, 1, 1, 1, 0],
  [1, 0, 1, 0, 0],
];

function reserveFirstAvailableSeat(seats) {
  rows: for (let i = 0; i < seats.length; i++) {
    columns: for (let j = 0; j < seats[i].length; j++) {
      if (seats[i][j] === 0) {
        seats[i][j] = 1; // Reserve the seat
        console.log(`Reserved seat at row ${i + 1}, column ${j + 1}`);
        break rows;
      }
    }
  }
}

reserveFirstAvailableSeat(seats);
```


<br />
<hr />

#### Issue 267 - SPOT THE BUG

```js
function getId(user, fallback) {
  return user && user.id ?? fallback;
}
```

#### SPOT THE BUG: SOLUTION
The ?? operator has higher precedence than the && operator. This means that the expression user && user.id ?? fallback is equivalent to user && (user.id ?? fallback). This is not what we want. We want to return fallback if user is null or undefined, and user.id otherwise.

To fix this, we need to use parentheses to change the order of evaluation:

```js
function getId(user, fallback) {
  return (user && user.id) ?? fallback;
}
```

or even better, just use optional chaining:

```js
function getId(user, fallback) {
  return user?.id ?? fallback;
}
```



<br />
<hr />

#### Issue 277 - SPOT THE BUG

```js
function reverseString(str) {
  return str.split("").reverse().join("");
}

let reversedString = reverseString("Hello, 👋!");
console.log(reversedString);
```

#### SPOT THE BUG: SOLUTION

This bug occurs because the split method treats the string as an array of 16-bit units, not as an array of characters resulting the unexpected output: !�� ,olleH. By using Array.from(str) or [...str] the string is split into an array of actual characters, respecting the surrogate pairs.

Using Array.from:
```js
function reverseString(str) {
  return Array.from(str).reverse().join("");
}

let reversedString = reverseString("Hello, 👋!");
console.log(reversedString);
```
Using the spread operator:

```js

function reverseString(str) {
  return [...str].reverse().join("");
}

let reversedString = reverseString("Hello, 👋!");
console.log(reversedString);
```
