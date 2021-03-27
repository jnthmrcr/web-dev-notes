# Regular Expressions
Regular expressions are used in programming languages to match parts of strings. You create patterns to help you do that matching.

If you want to find the word ```the``` in the string ```The dog chased the cat```, you could use the following regular expression: ```/the/```. Notice that quote marks are not required within the regular expression.

## test()

One way to test a regex in js is using the ```.test()``` method. The ```.test()``` method takes the regex, applies it to a string (which is placed inside the parentheses), and returns ```true``` or ```false``` if your pattern finds something or not.

```javascript
let myString = "Hello, World!";
let myRegex = /Hello/;
let result = myRegex.test(myString); // returns true

let myString2 = "hEllo, world!"
result = myRegex.text(myString2); // returns false
```
## OR operator
the ```alternation``` or ```OR``` operator: ```|``` can be used to check for two or more patterns.
```javascript
let petString = "James has a pet cat.";
let petRegex = /dog|cat|bird|fish/; // Change this line
let result = petRegex.test(petString);
```
## i flag
appending the ```i``` flag to the regex ignores case 
```javascript
let myString = "freeCodeCamp";
let fccRegex = /freecodecamp/i; //matches FREECODECAMP FreeCodeCamp
let result = fccRegex.test(myString);
```

# Extract Matches

reverse of ```.test()```, apply ```.match()``` to string to see if argument exists within string. returns that string if found.
```javascript
let extractStr = "Extract the word 'coding' from this string.";
let codingRegex = /coding/;
let result = extractStr.match(codingRegex); // returns "coding"
```

## g flag

To search or extract a pattern more than once, you can use the ```g``` flag.
```javascript

let repeatRegex = /Repeat/g;
testStr.match(repeatRegex); // returns ["Repeat", "Repeat", "Repeat"]
```
can combine flags:
```javascript
let twinkleStar = "Twinkle, twinkle, little star";
let starRegex = /twinkle/gi; // Change this line
let result = twinkleStar.match(starRegex); // Twinkle twinkle
```
