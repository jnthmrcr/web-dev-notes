# Javascript Notes

variables are ```undefined``` upon declaration
>*(boo~!, untyped variables)*

math operations on ```undefined``` results in ```NaN``` "not a number"

variables are camelCase

Number is a datatype... wat?

```i++``` and ```i--``` is still a thing
>thank god

decimals are floats? so ```5.2``` is a float

not sure if ```5.0``` is a float

```%``` is the *remainder* operator, not the *modulus* operator because it works different with negative numbers
>jank ass javascript

```+=``` and ```-=``` and ```*=``` and ```/=``` are a thing
>civilized

# escape characters

| code | output |
|:---:|:---|
| ```\'``` | single quote    |
| ```\"``` | double quote    |
| ```\\``` | backslash       |
| ```\n``` | newline         |
| ```\r``` | carriage return |
| ```\t``` | tab             |
| ```\b``` | word boundary   |
| ```\f``` | form feed       |

```javascript
var sampleStr = "Alan said, \"Peter is learning JavaScript\".";
```
```\"``` is used to insert quote marks within a string

```javascript
conversation = 'Finn exclaims to Jake, "Algebraic!"';
```
alternating quote types is also a strategy

this is important when definding html tags
```javascript
var myStr = '<a href="http://www.example.com" target="_blank">Link</a>';
```

```String``` can be treated like a char array
```javascript
var firstName = "Charles";
var firstLetter = firstName[0]; // firstLetter is "C"
```

except they is *immutable*, cannot be altered after creation. the variable holding a string can, however, be changed

can get length of a string with ```.length```
# Arrays

arrays can hold stuff of different types, including other arrays, to make a multidimentional array

arrays *are mutabe* so you can do this:
```javascript
var ourArray = [50,40,30];
ourArray[0] = 15; // equals [15,40,30]
```

```.push(x)``` can be used to add data (x) to the end of an array

```.pop()``` returns the last index of an array and removes it from that array

```javascript
var threeArr = [1, 4, 6];
var oneDown = threeArr.pop();
console.log(oneDown); // Returns 6
console.log(threeArr); // Returns [1, 4]
```

```.shift()``` works like pop except it returns and removes the first index of an array

```.unshift(x)``` is like push but it adds elements to the front of an array

> okay this is actually dumb now, you have multiple methods doing the same shit. just make some goddamn overloads

The Array#join() function creates a new string from concatenating all elements in an array. For example:
```javascript
['Hello', ' ', 'World'].join(''); // 'Hello World'
```
The first parameter to join() is called the separator. By default, the separator is a single comma ','. But you can pass in any separator you want. for example, "/" for URL fragments
```javascript
['a', 'b', 'c'].join(); // 'a,b,c'
// 'Twas the night before Christmas'
['Twas', 'the', 'night', 'before', 'Christmas'].join(' ');
// 'masteringjs.io/tutorials/fundamentals/string-concat'
['masteringjs.io', 'tutorials', 'fundamentals', 'string-concat'].join('/');
```
# Functions

functions look like this:

```javascript
function testFun(param1, param2) {
  console.log(param1, param2);
}
```

you may or may not be able to define a global variable without a ```var``` its not clear.

```return``` returns, dont need a declaration in the signature

functions without a ```return``` return a value of ```undefined```

Strict equality ```===``` is the counterpart to the equality operator ```==```. However, unlike the equality operator, which attempts to convert both values being compared to a common type, the strict equality operator does not perform a type conversion.

```javascript
3 === 3   // true
3 === '3' // false
3 == 3    // true
3 == '3'  // true

// same goes for nonequal
1 !=  2     // true
1 != "2"    // true

3 !==  3   // false
3 !== '3'  // true
4 !==  3   // true

```

```typeof``` can determine the type of a variable

```case``` values are tested with strict equality ```===```

# Objects (JSON)

Objects are similar to arrays, except that instead of using indexes to access and modify their data, you access the data in objects through what are called properties.
> feels like kvp, dictionaries/hashmaps

```javascript
var cat = {
  "name": "Whiskers",
  "legs": 4,
  "tails": 1,
  "enemies": ["Water", "Dogs"]
};
```
properties get typecasted to strings if you dont manually do this

properties can be accessed with dot notation ```.``` or bracket notation ```[]``` bracket notation is required if a property has a space in its name

```javascript
var myObj = {
  prop1: "val1",
  prop2: "val2"
};
var prop1val = myObj.prop1; // val1
var prop2val = myObj["prop2"]; // val2
```

```javascript
var someObj = {
  propName: "John"
};
function propPrefix(str) {
  var s = "prop";
  return s + str;
}
var someProp = propPrefix("Name"); // someProp now holds the value 'propName'
console.log(someObj[someProp]); // "John"
```

you can add and delete properties after object creation

```javascript
var ourDog = {
  "name": "Camper",
  "legs": 4,
  "tails": 1,
  "friends": ["everything!"],
  "bark": "bow-wow"
};

outDog.paws = "toe beans" // new property "paws"
delete ourDog.bark; // deleted property "bark"
```

can check if property exists with .hasOwnProperty(x)
```javascript
objects can be used in place of switches/elseif statements if all inputs are known

var myObj = {
  top: "hat",
  bottom: "pants"
};
myObj.hasOwnProperty("top");    // true
myObj.hasOwnProperty("middle"); // false
```

> This is just json fuck my life

> "javascript object notation" fuck my life

can store data and shit idk

```javascript
var ourStorage = {
  "desk": {
    "drawer": "stapler"
  },
  "cabinet": {
    "top drawer": { 
      "folder1": "a file",
      "folder2": "secrets"
    },
    "bottom drawer": "soda"
  }
};
ourStorage.cabinet["top drawer"].folder2;  // "secrets"
ourStorage.desk.drawer; // "stapler"
```

# iterating (loops/recursion)
```for ([initialization]; [condition]; [final-expression])```

The condition statement is evaluated at the beginning of every loop iteration and will continue as long as it evaluates to true. When condition is false at the start of the iteration, the loop will stop executing. This means if condition starts as false, your loop will never execute.

recursion
all my homies hate recursion
```javascript
function multiply(arr, n) {
    var product = 1;
    for (var i = 0; i < n; i++) {
        product *= arr[i];
    }
    return product;
}
function multiply(arr, n) {
    if (n <= 0) {
        return 1;
    } else {
        return multiply(arr, n - 1) * arr[n - 1];
    }
}
```
Recursive functions must have a base case when they return without calling the function again (in this example, when n <= 0), otherwise they can never finish executing.

```javascript
function rangeOfNumbers(startNum, endNum) {
  if (startNum == endNum) {
    return [startNum];
  } else {
    const arr = rangeOfNumbers(startNum, endNum - 1);
    arr.push(endNum);
    return arr;
  }
};
```
> goes from start num to end

# Random

```Math.random()``` generates a random decimal number between 0 (inclusive) and not quite up to 1 (exclusive).

random range:

```javascript
Math.floor(Math.random() * (max - min + 1)) + min
```

```parseInt()``` parses a string and returns an integer.
```javascript
var a = parseInt("007"); // returns int 7
```
It takes a second argument for the radix, which specifies the base of the number in the string. The radix can be an integer between 2 and 36.
```javascript
var a = parseInt("11", 2); // returns int 3
```

``` javascript
function findGreaterOrEqual(a, b) {
  if (a === b) {
    return "a and b are equal";
  }
  else if (a > b) {
    return "a is greater";
  }
  else {
    return "b is greater";
  }
}
```
The above function can be re-written using multiple conditional operators:
```javascript
function findGreaterOrEqual(a, b) {
  return (a === b) ? "a and b are equal" 
    : (a > b) ? "a is greater" 
    : "b is greater";
}
```