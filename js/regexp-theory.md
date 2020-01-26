## Regexp Theory

A Regular Expression, or RegEx, is a pattern used to match character combinations in a string.
A regular expression literal is a RegEx pattern enclosed within forward slashes:

```js
const re = /ab+c/;
```

This RegEx above matches the character `a`, followed by one or more instances of the character `b`, followed by the character `c`.

We can write a regular expression string and pass it as an argument to the RegExp constructor:

```js
const re = new RegExp("ab+c");
```

### Flags

To create a RegExp object, we use this syntax:

```js
new RegExp(pattern[, flags])
```

To create a regular expression literal, we use this syntax:

```
/pattern/flags;
```

If specified, flags can have any combination of the following values:

- `g`: global match.
- `i`: ignore case.
- `m`: multiline. Treats beginning (^) and end (\$) characters as working over multiple lines.
- `u`: unicode. Treat pattern as a sequence of unicode code points.
- `y`: sticky. Matches only from the index indicated by the lastIndex property of this regular expression in the target string.

### Special Characters in Regular Expressions

#### Character Classes

Special commands used to match a single character from some input string. Here are the basic forms:

- Enclosed within square brackets. Specify the what you'd like your expression to match within square brackets; for example, `[a-f]` will match any lowercase a through f character.
- Predefined: These consist of a backslash character (\) followed by a letter. The table below shows some predefined character classes and the characters they match.

Those are:

- `.`: The period matches any single character, except line terminators (e.g., a newline).
- `\d`: A single digit character (i.e., [0-9]).
- `\D`: A single non-digit character (i.e., [^0-9]).
- `\w`: A single alphanumeric word character, including the underscore (i.e., [A-Za-z0-9_]).
- `\W`: A single non-word character (i.e., [^a-za-z0-9_]).
- `\s`: A single whitespace character. This includes space (), tab (\t), form feed, line feed, and other Unicode spaces.
- `\S`: A single non-whitespace character (i.e., [^\w]).

### Character Sets

- The character set [abcd] will match any one character from the set {a, b, c, d}. This is equivalent to [a-d].
- The character set [^abcd]: Matches anything other than the enclosed characters. This is equivalent to [^a-d].

#### Alteration

We use the `|` symbol to match one thing or the other. For example, `a|b` matches either `a` or `b`.

#### Boundaries

Boundaries are:

- `^`: Matches beginning of input. If the multiline flag is set to true, also matches immediately after a line break character.
- `\$`: Matches end of input. If the multiline flag is set to true, also matches immediately before a line break character.
- `\b`: A zero-width word boundary, such as between a letter and a space.
- `\B`: Matches a zero-width non-word boundary, such as between two letters or between two spaces.

#### Grouping and back references

- `(a)`: Matches a and remembers the match. These are called capturing groups.
- `(?:a)`: Matches a but does not remember the match. These are called non-capturing groups.
- `\n`: Here n is a positive integer. A back reference to the last substring matching the n parenthetical in the regular expression.

#### Quantifiers

- `a*`: Matches the preceding item a, 0 or more times.
- `a+`: Matches the preceding item a, 1 or more times.
- `a?`: Matches the preceding item a, 0 or 1 time.
- `a{n}`: Here n is a positive integer. Matches exactly n occurrences of the preceding item a.
- `a{n, }`: Here n is a positive integer. Matches at least n occurrences of the preceding item a.
- `a{n, m}`: Here n and m are positive integers. Matches at least n and at most m occurrences of the preceding item a.

#### Assertions

- `a(?=b)`: Matches a only if a is followed by b.
- `a(?!b)`: Matches a only if a is not followed by b.

### Working with Regular Expressions

### RegExp methods: test

The test() method executes a search for a match between a regular expression and a specified string. Returns true or false.

```js
var re = /^learn/;
var str1 = "learn regular expressions";
console.log(re.test(str1)); // true
```

### RegExp methods: exec

The exec() method executes a search for a match in a specified string. Returns a result array or null.

```js
var re = /quick\s(brown).+?(jumps)/gi;
var str = "The Quick Brown Fox Jumps Over The Lazy Dog.";
var res = re.exec(str);

// The result object contains following information:
// 1. [0] is the full string of characters matched
// 2. [1], ...[n] is the parenthesized substring matches, if any. The number of possible parenthesized substrings is unlimited.
// 3. index is the 0-based index of the match in the string.
// 4. input is the original string.
```

The result is definitely weird :)

### String methods: match

The match() method retrieves the matches when matching a string against a regular expression.

```js
var re = /see (chapter \d+(\.\d)*)/i;
var str =
  "For more information on regular expressions, see Chapter 3.4.5.1 and CHAPTER 2.3";

console.log(str.match(re));

// [
//     'see Chapter 3.4.5.1',
//     'Chapter 3.4.5.1',
//     '.1',
// ]
// index: 45,
// input: 'For more information on regular expressions, see Chapter 3.4.5.1 and CHAPTER 2.3',
// groups: undefined
```

### String methods: search

The search() method executes a search for a match between a regular expression and this String object. If successful, search() returns the index of the first match of the regular expression inside the string. Otherwise, it returns -1.

```js
const re = /learn/;
const str1 = "Today, we'll learn about regular expressions.";

console.log("A search for", re, "returns", str1.search(re), "\n"); // 13
```

### String methods: split

The split() method splits a String object into an array of strings by separating the string into substrings. Separator specifies the character(s) to use for separating the string. The separator is treated as a string or a regular expression. If separator is omitted, the array returned contains one element consisting of the entire string. If separator is an empty string, str is converted to an array of characters.

```js
const name = "Julia Roberts";
const res = name.split(" ");

console.log("The split array:", res); // ["Julia", "Roberts"]
console.log("First Name:", res[0]); // Julia
console.log("Last Name:", res[1]); // Roberts
```

### String methods: replace

The `replace(pattern, replacement)` method returns a new string where some (or all) occurrences of a matched have been replaced with a substring.

- `pattern` : This value can be a string or a RegExp object to match against the calling string.
- `replacement`: This value can be a substring to replace the match with, or it can be a function to invoke that generates the replacement substring.
