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
# case insensitive (i) flag
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

# global (g) flag

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
# wildcard (.) character

The wildcard character ```.``` will match any one character

You can use the wildcard character just like any other character in the regex

```/hu./``` will match ```hug```, ```huh```, ```hut```

# character classes
You can search for a literal pattern with some flexibility with character classes. Character classes allow you to define a group of characters you wish to match by placing them inside square ([ and ]) brackets.

For example, you want to match ```bag```, ```big```, and ```bug``` but not ```bog```. You can create the regex ```/b[aiu]g/``` to do this. The ```[aiu]``` is the character class that will only match the characters ```a```, ```i```, or ```u```.

Inside a character set, you can define a range of characters to match using a hyphen character: ```-```

```javascript
let catStr = "cat";
let batStr = "bat";
let matStr = "mat";
let bgRegex = /[a-e]at/;
catStr.match(bgRegex); // returns ["cat"]
batStr.match(bgRegex); // returns ["bat"]
matStr.match(bgRegex); // returns null
```

hyphen can match numbers too!
```javascript
let jennyStr = "Jenny8675309";
let myRegex = /[a-z0-9]/ig;
jennyStr.match(myRegex); // returns an array of everything basically
```

# negated character sets
you could also create a set of characters that you do not want to match. To create a negated character set, you place a caret character (```^```) after the opening bracket and before the characters you do not want to match.

For example, ```/[^aeiou]/gi``` matches all characters that are not a vowel. Note that characters like `.`, `!`, `[`, `@`, `/` and white space are matched - the negated vowel character set only excludes the vowel characters.

# multiple characters
You can use the ```+``` character to check if a character (or group of characters) that appears one or more times in a row

For example, `/a+/g` would find one match in `abc` and return `["a"]`. Because of the `+`, it would also find a single match in `aabc` and return `["aa"]`.
```javascript
let difficultSpelling = "Mississippi";
let myRegex = /s+/g;
let result = difficultSpelling.match(myRegex); // ['ss','ss']
```

# Characters that Occur Zero or More Times
You can use the ```*``` character to check if a character (or group of characters) that appears zero or more times in a row
```javascript
let soccerWord = "gooooooooal!";
let gPhrase = "gut feeling";
let oPhrase = "over the moon";
let goRegex = /go*/;
soccerWord.match(goRegex); // ["goooooooo"]
gPhrase.match(goRegex); // ["g"]
oPhrase.match(goRegex); // null

let chewieQuote = "Aaaaaaaaaaaaaaaarrrgh";
let chewieRegex = /Aa*r+g+h+/;
```

