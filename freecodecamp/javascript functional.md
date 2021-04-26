Functional programming is a style of programming where solutions are simple, isolated functions, without any side effects outside of the function scope: `INPUT -> PROCESS -> OUTPUT`

Functional programming is about:
- Isolated functions - there is no dependence on the state of the program, which includes global variables that are subject to change
- Pure functions - the same input always gives the same output
- Functions with limited side effects - any changes, or mutations, to the state of the program outside the function are carefully controlled

## callbacks
`Callbacks` are the functions that are slipped or passed into another function to decide the invocation of that function. You may have seen them passed to other methods, for example in `filter`, the callback function tells JavaScript the criteria for how to filter an array.

## first class functions
Functions that can be assigned to a variable, passed into another function, or returned from another function just like any other normal value, are called `first class` functions. In JavaScript, all functions are first class functions.

## higher order functions
The functions that take a function as an argument, or return a function as a return value are called higher order functions.

## lambda
When the functions are passed in to another function or returned from another function, then those functions which gets passed in or returned can be called a lambda.

```javascript
const prepareGreenTea = () => 'greenTea';
const prepareBlackTea = () => 'blackTea';

const getTea = (prepareTea, numOfCups) => {
  const teaCups = [];

  for(let cups = 1; cups <= numOfCups; cups += 1) {
    const teaCup = prepareTea();
    teaCups.push(teaCup);
  }
  return teaCups;
};

const tea4GreenTeamFCC = getTea(prepareGreenTea, 27); // 27 'greenTea'
const tea4BlackTeamFCC = getTea(prepareBlackTea, 13); // 13 'blackTea'
```

# Imperitive code

In English (and many other languages), the imperative tense is used to give commands. Similarly, an imperative style in programming is one that gives the computer a set of statements to perform a task.

> okay i straight up did not understand the example they gave but it was over complicated and hurt my feelings so idk. "imperitive bad" or something. i guess.

> oh, okay, so, the issue, was the function they used, was a bad function, that changed stuff when it shouldn't have. so... fml...

This is a small example of a much larger pattern - you call a function on a variable, array, or an object, and the function changes the variable or something in the object.

One of the core principles of functional programming is to not change things. Changes lead to bugs. It's easier to prevent bugs knowing that your functions don't change anything, including the function arguments or any global variable.

in functional programming, changing or altering things is called *mutation*, and the outcome is called a *side effect*. A function, ideally, should be a *pure function*, meaning that it does not cause any *side effects*.

Another principle of functional programming is to always declare your dependencies explicitly. This means if a function depends on a variable or object being present, then pass that variable or object directly into the function as an argument.

There are several good consequences from this principle. The function is easier to test, you know exactly what input it takes, and it won't depend on anything else in your program.

This can give you more confidence when you alter, remove, or add new code. You would know what you can or cannot change and you can see where the potential traps are.

Finally, the function would always produce the same output for the same set of inputs, no matter what part of the code executes it.


So far, we have seen two distinct principles for functional programming:

- Don't alter a variable or object - create new variables and objects and return them if need be from a function. Hint: using something like var newArr = arrVar, where arrVar is an array will simply create a reference to the existing variable and not a copy. So changing a value in newArr would change the value in arrVar.
> use `let retList = [...origList]` to copy a list
- Declare function parameters - any computation inside a function depends only on the arguments passed to the function, and not on any global object or variable.


 Functions are considered *first class objects* in JavaScript, which means they can be used like any other object. They can be saved in variables, stored in an object, or passed as function arguments.

# map()
`Array.prototype.map()`

The `map` method iterates over each item in an array and returns a new array containing the results of calling the callback function on each element. It does this without mutating the original array.

When the callback is used, it is passed three arguments. The first argument is the current element being processed. The second is the index of that element and the third is the array upon which the map method was called.

```javascript
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const names = users.map(user => user.name);
console.log(names); // [ 'John', 'Amy', 'camperCat' ]
```
`map` method returns an array of the same length as the one it was called on. It also doesn't alter the original array, as long as its callback function doesn't.
```javascript
.map(movie => {
    return {
        title: movie.Title,
        rating: movie.imdbRating
    };
})
```
in this example, it didn't work without the `return` keyword. i guess objects arn't values? javascript is fucking stupid.
# filter()
`filter` calls a function on each element of an array and returns a new array containing only the elements for which that function returns `true`. In other words, it filters the array, based on the function passed to it. Like `map`, it does this without needing to modify the original array.

The callback function accepts three arguments. The first argument is the current element being processed. The second is the index of that element and the third is the array upon which the filter method was called.

```javascript
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];

const usersUnder30 = users.filter(user => user.age < 30);
console.log(usersUnder30); // [{name:'Amy',age: 20},{name:'camperCat',age:10}]
```

# Concat()
```javascript
[1, 2, 3].concat([4, 5, 6]); // [1, 2, 3, 4, 5, 6]
```
`concat` combines arrays into a new one without mutating the original arrays.

`push` adds an item to the end of the same array it is called on, which mutates that array.

# reduce()
`Array.prototype.reduce()` is the most general of all array operations in JavaScript. You can solve almost any array processing problem using the `reduce` method.

The `reduce` method allows for more general forms of array processing, and it's possible to show that both `filter` and `map` can be derived as special applications of `reduce`. The `reduce` method iterates over each item in an array and returns a single value (i.e. string, number, object, array). This is achieved via a callback function that is called on each iteration.

The callback function accepts four arguments. The first argument is known as the accumulator, which gets assigned the return value of the callback function from the previous iteration, the second is the current element being processed, the third is the index of that element and the fourth is the array upon which `reduce` is called.

In addition to the callback function, `reduce` has an additional parameter which takes an initial value for the accumulator. If this second parameter is not used, then the first iteration is skipped and the second iteration gets passed the first element of the array as the accumulator.

```javascript
const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];
const sumOfAges = users.reduce((sum, user) => sum + user.age, 0);
console.log(sumOfAges); // 64

const users = [
  { name: 'John', age: 34 },
  { name: 'Amy', age: 20 },
  { name: 'camperCat', age: 10 }
];
const usersObj = users.reduce((obj, user) => {
  obj[user.name] = user.age;
  return obj;
}, {});
console.log(usersObj); // { John: 34, Amy: 20, camperCat: 10 }
```
> yeah i dont like this

> just use a fucking `for` loop ffs

```javascript
function getRating(watchList){
  let averageRating = watchList.filter(x => x.Director === "Christopher Nolan")
    .reduce((total, film, index, array) =>
    {
      total += Number(film.imdbRating);
      console.log(total);
      if( index === array.length-1) { 
        return total/array.length;
      } else { 
        return total;
      }
    }, 0); // without this zero, total is set to a string or something idk. i hate javascript
  return averageRating;
}
console.log(getRating(watchList)); //8.675
```

# Sort
The `sort` method sorts the elements of an array according to the callback function. JavaScript's default sorting method is by string Unicode point value, which may return unexpected results. Therefore, it is encouraged to provide a callback function to specify how to sort the array items.
```javascript
function ascendingOrder(arr) {
  return arr.sort(function(a, b) {
    return a - b;
  });
}
ascendingOrder([1, 5, 2, 3, 4]); // [1, 2, 3, 4, 5]

function reverseAlpha(arr) {
  return arr.sort(function(a, b) {
    return a === b ? 0 : a < b ? 1 : -1;
  });
}
reverseAlpha(['l', 'h', 'z', 'b', 's']); // ['z', 's', 'l', 'h', 'b']
```
`sort` mutates the array its called on. One way to avoid this is to first concatenate an empty array to the one being sorted (`slice` & `concat`)
```javascript
var globalArray = [5, 6, 3, 2, 9];
function nonMutatingSort(arr) {
  return arr.slice(0, arr.length).sort((a,b) => a-b);
}
console.log(nonMutatingSort(globalArray)); // [ 2, 3, 5, 6, 9 ]
```

# .split()
The `split` method splits a string into an array of strings. It takes an argument for the delimiter, which can be a character to use to break up the string or a regular expression. For example, if the delimiter is a space, you get an array of words, and if the delimiter is an empty string, you get an array of each character in the string.
```javascript
function splitify(str) {
  return str.split(/\W/)
}
console.log(splitify("Hello World,I-am code")); // [ 'Hello', 'World', 'I', 'am', 'code' ]
```

# .join()
The `join` method is used to join the elements of an array together to create a string. It takes an argument for the delimiter that is used to separate the array elements in the string.
```javascript
function sentensify(str) {
  return str.split(/\W/).join(' ');
}
sentensify("May-the-force-be-with-you"); // May the force be with you

function urlSlug(title) {
  return title.toLowerCase().split(" ").filter(x => x != "").join("-");
}
urlSlug(" Winter Is  Coming") // winter-is-coming
```

# .every()
The `every` method works with arrays to check if *every* element passes a particular test. It returns a Boolean value - `true` if all values meet the criteria, `false` if not.
```javascript
function checkPositive(arr) {
  return arr.every(x => x > 0) // is every element positive?
}
checkPositive([1, 2, 3, -4, 5]); // false
```

# .some()
The `some` method works with arrays to check if any element passes a particular test. It returns a Boolean value - `true` if any of the values meet the criteria, `false` if not.
```javascript
function checkPositive(arr) {
  return arr.some(x => x > 0)
}
checkPositive([1, 2, 3, -4, 5]); // true
```

# Currying
>dont like the look of this

The *arity* of a function is the number of arguments it requires. *Currying* a function means to convert a function of N arity into N functions of arity 1.

In other words, it restructures a function so it takes one argument, then returns another function that takes the next argument, and so on.

This is useful in your program if you can't supply all the arguments to a function at one time. You can save each function call into a variable, which will hold the returned function reference that takes the next argument when it's available.
```javascript
var funcForY = curried(1);
console.log(funcForY(2)); // 3
```
Similarly, partial application can be described as applying a few arguments to a function at a time and returning another function that is applied to more arguments.
```javascript
function impartial(x, y, z) {
  return x + y + z;
}
var partialFn = impartial.bind(this, 1, 2);
partialFn(10); // 13
```
```javascript
function add(x) {
  return (y) => {
    return (z) => {
      return x + y + z;
    }
  }
}
// or
function add(x) {
  return y => z => x + y + z;
}
add(10)(20)(30);