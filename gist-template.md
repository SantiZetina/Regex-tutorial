# Regex Tutorial: Validating A US Phone Number

In this tutorial, we will explore how to use regex to validate a US phone number, which consists of then digits arragned in a specific format. 

## Summary

We will be describing a regex that can be used to validate a US phone number. The regex pattern is designed to match a ten-digit US number arranged in a specific format. The pattern utilizes a combination of character classes, groups, and anchors to match the desired format. Here is the regex pattern:

^\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}$

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

### Anchors

Anchors are special characters that match a specific position within a string. Anchors do not match any characters themselves, but they are used to specify the beginning or end of a line, word, or string. In our US phone number regex, the anchors used are `^` and `$`.

* The caret `^` matches the start of a string and is used to indicate that the following pattern should appear at the beginning of the string. 

 * The dollar sign `$` matches the end of a string and is used to indicate that the preceding pattern should appear at the end of the string.

These anchors are used to ensure that the regular expression matches the entire phone number string and does not allow for any characters before or after the phone number.

`^`\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}`$`


### Quantifiers

Quantifiers are special characters that allow you to specify how many times a preceding character or group of characters should be matched. Quantifiers can be used to make a pattern match more flexible and versatile, by allowing it to match a varying number of characters.

Some of the most common quantifiers used in regex:

* `*`: Matches the preceding character or group zero or more times. For example, the regex `ab*c` would match "ac", "abc", "abbc", "abbbc" and so on. 
    
 * `+`: Matches the preceding character or group one more more times. For example, the regex `ab+c` would match "abc", "abbc", "abbbc" and so on, but would not match "ac". 

 * `?`: Matches the preceding chracter or group zero or one time. For example, the regex `colou?r` would match "color: or "colour".

 * `{n}`: Matches the preceding character or group exaclty n times. For example, the regex `a{3}` would match "aaa".

* `{n,}`: Matches the preceding character or group at least n times. For example, the regex `a{3,}` would match "aaa", "aaaa", "aaaaa", and so on. 

 * `{n,m}`: Matches the preceding character or group at least n times and at most m times. For example, the regex `a{2,4}` would match "aa", "aaa", or "aaaa", but would not match "a" or "aaaaa"

There are several quantifiers used in our US phone validator specifiying the number of times a certain pattern should match:

   * `{3}`: Matches the preceeding `\d`(digit) character exaclty three times, representing the three digits in an area code. 

* `{4}`: Matches the preceeding `\d`(digit) character exactly four times, representing the four digits in the phone number. 

* `?`: Matches the preceding pattern zero or one time. This is used to make the opening and closing parantheses optinal in the area code section of the phone number. 

* `[-.\s]?`: Matches the character class `[-.\s]` (dash, dot, or space) zero or one time, representing the optional separator between the area code and the phone number 

^\(`?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}`$

### Grouping Constructs

Grouping constructs are used to group a sequence of characters or patterns together and treat them as a single unit. Grouping constructs are useful for applying quantifiers, alternation, and other operations to a group of characters as a whole, rather than to individual characters. 

There are two main types of grouping constructs in regular expressions:

1. Capturing Groups: Capturing groups are created using parentheses `()` and allow you to capture and extract a specific portion of the matches string. When a regular expression containing capturing group is matched against a string, the captrued substrings can be accessed and used in various ways. 
    For example, the regular expression `(\d{3}-(\d{4}))` matches a string in the format of a US zip code and captures teh first three digits and the last four digits as two seperate groups.

2. Non-capturing groups: Non-capturing groups are created using the syntax `(?: )` and are smiliar to capturing groups, but do not capture and store the matched substring as a separate group. Non-capturing groups are used to group a sequence of characters together without capturing a separate substring. 
    For example, the regular expression `a(?:bc|def)g` matches "abcg" or "adefg" and groups the sequence "bc" or "def" together, but does not capture it as a separate group. 

In our US phone number validator regex, there are two groups used to extract the area code and phone number separately:

1. `(\d{3})`: This capturing group matches three digits and captures them as the area code. The opening and closing parentheses create a capturing group that allows you to extract the matched digits. 

2. `(\d{3}-\d{4})`: The capturing group matches seven digits in the format of a phone number, separated by a dash, and captures them as the phone number. 

^\(?`\d{3}`\)?[-.\s]?\d{3}[-.\s]?\d{4}$


### Bracket Expressions

Bracket Expressions (a special kind of character class) allows us to specify a set or range of characters to match. Bracket expressions are enclosed in square brackets `[ ]` and can match any sinlge character that appears within the brackets. For example, the bracket expression `[aeiou]` matches any sinlge lowercase vowel, while the expressions `[0-9]` matches any sinlge digit from 0 to 9.
Bracket expressions can be used with various regular expression operations, such as quantifiers and anchors, to match specific patterns of charactes within a string. 

In our US phone number validator regular expression, bracket expression are used to match certain characters that may appear in a US phone number. Specifically, the expression includes the following bracket expression. 

1. `[-.\s]?`: This bracket expression matches a single character that is either a dash, period, or space. The question mark makes this entire expression optional, allowing a valid phone number to contain zero or one of these characters. 

2. `[()]?`: This bracket expression matches a sinlge character that is either an opening or closing parenthesis. The question mark makes this entire expression optional, allowing a valid phone number to contain zero or one of these characters. 

The bracket expressions are used in combination with other regular expression elements, such as capturing groups and anchors, to match the specific format of a vaild US phone number.

^\(?\d{3}\)?`[-.\s]?`\d{3}`[-.\s]?`\d{4}$


### Character Classes

Character classes is a way of specifying a group or range of characters that can be matched. Character classes are enclosed within square brackets `[ ]` and can  match any sinlge character that appears within the bracket. 

There are several pre-defined character classes that are commonly used in regular expressions, including:

 * `[a-z]`: Matches any single lowercase letter from a to z

* `[A-Z]`: Matches any sinlge uppercase letter from A to Z

* `.`: Matches any sinlge character except for a newline 

 * `\w`: Matches any word character (letters, digits, and underscores)

 * `\s`: Matches any whitespace character (spaces, tabs, newlines, etc)

 * `\d`: Matches any digit character

In our US phone number validator regex, character classes are used to match specific sets of characters that can appear in a phone number. For example:

1. `[0-9]`: This character class matches any single digit from 0 to 9, which is used to match the digits in the phone number.

2. `[a-zA-Z]`: This character class matches any sinlge uppercase or lowercase letter, which is used to match any letters that may be present in the phone number, such as the "O" in 1-800-CALL_NOW.

### The OR Operator

The OR operator, represented by the vertical bar `|`, is a regular expression operator that allows you to match one pattern or another. It matches either the pattern on the left or the pattern on the right. 

For example, the regular expression `cat|dog` would match either the word "cat" or the word "dog" in a given string. So if the input string is "I have a cat and a dog", the regular expression would match "cat" and "dog".

In the US phone number validator regular expression, the OR operator is used to match the diffrent variation of the phone number format. Specifically, the expression includes the following OR operator: 

1. `|`: This operator is used to match either a dash `-` or a period `.` in between the digits of the phone number. This allows the regular expression to match phone numbers with different delimiters, such as `(123) 456-7890` and `123.456.7890`. 

For example, the regular expression `(\\d{3})[-.]?(\\d{3})[-.]?(\\d{4})` matches a phone nnumber that consists of three digits, followed by either a dash or a period followed by three more digits, another dash or period, and finally four more digits

### Flags

Flags are used in regular expressions to modify how the pattern matching works. They are additional parameters that you can add to the regular expression to change the way it behaves. 

Some common flags include:

* `i`: This flag makes the regular expression case-insensitive, so that it matches both uppercase and lowercase letters.

* `g`: This flag enables global matching so that the regular expression matches all occurrences of the pattern in the input string, rather than just the first one.

* `m`: This flag enables multiline mode, so that the `^` and `$` anchors match the beginning and end of each line within the input string, rather than just the beginning and end of the entire input string. 

### Character Escapes

Character escapes are a feature of regular expressions that allow you to match special characters or sequences of characters that have a special meaning in the regular expression syntax. These special characters are referred to as metacharacters, and include characters like `.`, `*`, `?`, `|`, `(`, `)`, `[`, `]`, `{`, `}`, and `\`. 

By using a backlash followed a metacharacter, you can match the literal character rather than the special meaning of the metacharacter. For example, the regular expression `\\.` matches a literal period character rather than the speical meaning of the `.` metacharacter. 

## Author

Auhtor: Santiago Zetina 

GitHub: [GitHub](https://github.com/SantiZetina)