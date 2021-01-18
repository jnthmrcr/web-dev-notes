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