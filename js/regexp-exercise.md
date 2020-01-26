## Exercise

Complete the vowelsAndConsonants function. It has one parameter, a string, , consisting of lowercase English alphabetic letters (i.e., a through z). The function must do the following:

First, print each vowel in on a new line. The English vowels are a, e, i, o, and u, and each vowel must be printed in the same order as it appeared in .
Second, print each consonant (i.e., non-vowel) in on a new line in the same order as it appeared in .

#### Answer

```js
function vowelsAndConsonants(s) {
  var vowels = s.match(/[aeiou]/gi);
  var consonants = s.match(/[^aeiou]/gi);
  [...vowels, ...consonants].forEach(l => console.log(l));
}
```

#### Important

`^` is the character for `not`

## Exercise

Find a substring of length greater than 1 that starts and ends with same character.

#### Answer

```js
const re = /(.).*\1/;

"wxysz".match(re); // null
"wxyzw".match(re); // [0] wxyzw
"wxyzx".match(re); // [0] xyzx
"wxywz".match(re); // [0] wxyw
```

### Important

```js
const re = /(.).*\1/;
```

To note `\1` which is a backreference, means is the result of `(.)`
