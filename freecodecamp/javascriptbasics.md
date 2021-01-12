# Javascript Notes

``` === ``` is the comparison operator instead of ```==```

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

## escape characters

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

```String``` can be treated like a char array, except it is *immutable*, cannot be altered after creation. the variable holding a string can, however, be changed

can get length of a string with ```.length```
```javascript
var firstName = "Charles";
var firstLetter = firstName[0]; // firstLetter is "C"
```
