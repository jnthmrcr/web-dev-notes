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

# Replace
The `replace()` method returns a new string with some or all matches of a pattern replaced by a replacement. The pattern can be a string or a RegExp, and the replacement can be a string or a function to be called for each match. If pattern is a string, only the first occurrence will be replaced.
```javascript
const p = 'The quick brown fox jumps over the lazy dog. If the dog reacted, was it really lazy?';
console.log(p.replace('dog', 'monkey'));
// expected output: "The quick brown fox jumps over the lazy monkey. If the dog reacted, was it really lazy?"

function convertHTML(str) {
  let htmlChars = {
    "&":"&amp;",
    "<":"&lt;",
    ">":"&gt;",
    '"':"&quot;",
    "'":"&apos;"
  }
  return str.replace(/[&<>"']/g, x => htmlChars[x]);
}
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

# Greedy vs Lazy matching

a `greedy` match finds the longest possible part of a string that fits the regex pattern and returns it as a match. The alternative is called a `lazy` match, which finds the smallest possible part of the string that satisfies the regex pattern.

`?` switches to lazy matching
```javascript
let text = "<h1>Winter is coming</h1>";
let resultLazy = text.match(/<.*?>/); // "<h1>"
let resultGred = test.match(/<.*>/); // "<h1>Winter is coming</h1>"
```

# Match Beginning and Ending String Patterns
use `^` outside of character set to search for patterns at the beginning of strings.
```javascript
let rickyAndCal = "Cal and Ricky both like racing.";
let calRegex = /^Cal/;
let result = calRegex.test(rickyAndCal); // true
```

You can search the end of strings using the dollar sign character `$` at the end of the regex.
```javascript
let theEnding = "This is a never ending story";
let storyRegex = /story$/;
storyRegex.test(theEnding); // true
let noEnding = "Sometimes a story will have to end";
storyRegex.test(noEnding); // false
```

# shortcuts

## alphanumeric
>`\w`
```javascript
let longHand = /[A-Za-z0-9_]+/;
let shortHand = /\w+/;
```

## nonalphanumeric
>`\W`
```javascript
let longHand = /[^A-Za-z0-9_]/;
let shortHand = /\W/;
```

## digits
>`\d`
```javascript
let longHand = /[0-9]/;
let shortHand = /\d/;
```

## nondigits
>`\D`
```javascript
let longHand = /[^0-9]/;
let shortHand = /\D/;
```

## whitespace
>`\s`
```javascript
let longHand = /[\r\t\f\n\v]/;
let shortHand = /\s/;
```

## nonwhitespace
>`\S`
```javascript
let longHand = /[^ \r\t\f\n\v]/;
let shortHand = /\S/;
```

# wow cool
```javascript
let username = "JackOfAllTrades";
let userCheck = /^[a-z][a-z]+\d*$|^[a-z]\d\d+$/i;
let result = userCheck.test(username);
```

>- Usernames can only use alpha-numeric characters.
>- The only numbers in the username have to be at the end. There can be zero or more of them at the end. Username cannot start with the number.
>- Username letters can be lowercase and uppercase.
>- Usernames have to be at least two characters long. A two-character username can only use alphabet letters as characters.

# Quantity Specifiers
You can specify the lower and upper number of patterns with quantity specifiers

```javascript
let A4 = "aaaah";
let A2 = "aah";
let multipleA = /a{3,5}h/; // appearing between `3` and `5` times in the string `ah`
multipleA.test(A4); // true
multipleA.test(A2); // false
```
To only specify the lower number of patterns, keep the first number followed by a comma.
```javascript
let A4 = "haaaah";
let A2 = "haah";
let A100 = "h" + "a".repeat(100) + "h";
let multipleA = /ha{3,}h/; // minimum of 3 'a's
multipleA.test(A4); // true
multipleA.test(A2); // false
multipleA.test(A100); // true
```
```javascript
let multipleHA = /ha{3}h/; // only 3 'a's
```

# All or none
You can specify the possible existence of an element with a question mark, ?. This checks for zero or one of the preceding element. You can think of this symbol as saying the previous element is optional.
```javascript
let american = "color";
let british = "colour";
let rainbowRegex= /colou?r/;
rainbowRegex.test(american); // true
rainbowRegex.test(british); // true
```

# Positive and Negative Lookahead
positive lookahead will look to make sure the element in the search pattern is there, but won't actually match it.
>`(?=...)`

negative lookahead will look to make sure the element in the search pattern is not there
>`(?!...)`

```javascript
let quit = "qu";
let noquit = "qt";
let quRegex= /q(?=u)/;
let qRegex = /q(?!u)/;
quit.match(quRegex); // q, not qu
noquit.match(qRegex); // q
```
A more practical use of lookaheads is to check two or more patterns in one string. Here is a simple password checker that looks for between 3 and 6 characters and at least one number:
```javascript
let password = "abc123";
let checkPass = /(?=\w{3,6})(?=\D*\d)/;
checkPass.test(password);
```
>match passwords that are greater than 5 characters long

>and have two consecutive digits.
```javascript
let sampleWord = "abc123";
let pwRegex = /(?=\w{6,})(?=\w*\d{2})/; // ???
let result = pwRegex.test(sampleWord);
```

# Positive and Negative Lookbehind
Lookbehind has the same effect, but works backwards. It tells the regex engine to temporarily step backwards in the string, to check if the text inside the lookbehind can be matched there.

`(?<!a)b` matches a `“b”` that is not preceded by an `“a”`, using negative lookbehind.

It doesn’t match `cab`, but matches the `b` (and only the `b`) in `bed` or `debt`.

`(?<=a)b` (positive lookbehind) matches the `b` (and only the `b`) in `cab`, but does not match `bed` or `debt`.

The construct for positive lookbehind is `(?<=text)`: a pair of parentheses, with the opening parenthesis followed by a question mark, “less than” symbol, and an equals sign.
Negative lookbehind is written as `(?<!text)`, using an exclamation point instead of an equals sign. 

# Check For Mixed Grouping of Characters
```javascript
let testStr = "Pumpkin";
let testRegex = /P(engu|umpk)in/;
testRegex.test(testStr); // true

let myString = "Eleanor Roosevelt";
let myRegex = /(Franklin|Eleanor).*Roosevelt/; // allow for middle names
let result = myRegex.test(myString); // true, idk
```
# Capture Groups
Parentheses, `(` and `)`, are used to find repeat substrings. You put the regex of the pattern that will repeat in between the parentheses.

To specify where that repeat string will appear, you use a backslash (`\`) and then a number. This number starts at 1 and increases with each additional capture group you use. An example would be `\1` to match the first group.

>match a string that consists of only the same number repeated exactly three times separated by single spaces.
```javascript
let repeatNum = "42 42 42";
let reRegex = /^(\d+)\s\1\s\1$/;
// start, digits, space, same digits, space, same digits, end
let result = reRegex.test(repeatNum);
```

# Search and Replace
```javascript
let wrongText = "The sky is silver.";
let silverRegex = /silver/;
wrongText.replace(silverRegex, "blue"); // The sky is blue.

// access capture groups in the replacement string with dollar signs ($).
"Code Camp".replace(/(\w+)\s(\w+)/, '$2 $1'); // Camp Code

let str = "one two three";
let fixRegex = /(one)\s(two)\s(three)/;
let replaceText = "$3 $2 $1";
let result = str.replace(fixRegex, replaceText); // three two one

// trim whitespace at beginning and end
let hello = "   Hello, World!  ";
let wsRegex = /^\s+|\s+$/g;
let result = hello.replace(wsRegex, "");
```