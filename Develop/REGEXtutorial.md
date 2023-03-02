# REGEX Tutorial - Regular Expression Email Match

Welcome to my introductory to Regular Expressions also known as Regex. In this tutorial I will be providing you with a step by step tutorial on the basics and explain to you how you can match to any given email using Regex. I will explain to you why we use them, discuss how it works and guide you through the steps to get you started on your journey to using Regular Expressions.

## Summary
To familiarise yourself with what a Regex looks like, please take a look at the following:

 ```
 /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
 ```

At this stage this might just look like a sequence of random characters, but as you read on I will be breaking this down and explaining what each of the components of the following Regex mean. This Regex that I have chosen to introduce to you will enable you to ensure that a given email string matches a desired email template. Regex essentially is used to validate, search and edit input, configuring their characters and finding patterns.


## Table of Contents
- [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [OR Operator](#or-operator)
    - [Character Classes](#character-classes)
    - [Flags](#flags)
    - [Grouping and Capturing](#grouping-and-capturing)
    - [Bracket Expressions](#bracket-expressions)
    - [Greedy and Lazy Match](#greedy-and-lazy-match)
    - [Boundaries](#boundaries)
    - [Back-references](#back-references)
    - [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Author](#author)

## Regex Components
```
/^([a-z0-9_\.-]+)@([\da-z\.-]+)`\.`([a-z\.]{2,6})$/
```

 A regex is considered a literal, so the sequence of characters must be wrapped in slash characters `/`. Then essentially this Regex reads, 
 `^` start the string here with optionally `(` a string of character any where between a-z (lowercase), include any numbers 0-9, and any underscores, (literal) period, or hyphens which will matches 1 or more `[a-z0-9_\.-]+)`. Followed by an `@` character, then followed optionally by any digit, characters a-z, (literal) period, or hyphen which will matche 1 or more characters `([\da-z\.-]+)`. Followed by a (literal) period `\.` and another string optionally containing on 2-6 characters between a-z `([a-z\.]{2,6})` followed by `$` to indicate the end of the string. 

 Lets break it down.
### Anchors

The selected Regex uses two characters that represent the start and the end of the string, these are called *Anchors*. The beginning *Anchor* you will see is:
```
^
```
this marks the beginning position and will start the sting in that exact position, the character itself is typically called a caret.
At the near end of the Regex you will see:
```
$
```
which in opposite to the carrot indicates the end position, this is exactly where the string shall finish.

### Quantifiers
Regex quantifiers indicate numbers of characters or expressions to match, they define how many instances of a group, character, or character class must exist in the input to be considered a match. 

The quantifier `+` in our example:
```
([a-z0-9_\.-]+)
```
Indicates that to match, the string must have at least one of the following characters:

- `a-z`
- `0-9`
- `_`
- `-`
- `.`

Use the below as a basic reference:

```
        Matches -
*       : used to match a string that contains zero, one, or more occurrences
+       : used to match a string that contains one or more
?       : used to match a string containing zero or one occurrence
{n}     : used to match a string that contains n sequence of character in front
{n,}    : used to match a string that matches the complete number containing at least n number of digits
{n,m}   : used to match a sequence having atleast n and m number of digits (min, max)
n$      : used to match whether specified string ends with n or not
^n      : used to match if a specified string begins with n

        If any used above have the ? character after the quantifier it will make the quantifier "non-greedy", to explain more please proceed to the "Greedy and Lazy Match" section of this tutorial.
```
### OR Operator
The OR operator is simply symbolised by the following vertical line character:
```
|
```
In the example Regex, we dont use it but it is a useful component when using Regex as it will match any number of single characters which will allow for a either/or conditional matching.

Example
```
gr(a|e)y 
```
Will match both words; grey & gray. Which alternatively can be written like:
```
gr[ae]y
```
which uses Character Classes which you will see next.
### Character Classes
Character Classes are used to distinguish different characters, they will match any symbol from certain character sets. Such as distinguishing between letters and digits, whitespace or no whitespace. Below you will see the main basics you should learn:

```
\s: Whitespace
\S: Not whitespace
\w: Word
\W: Not a word
\d: Digit
\D: Not a digit
```
In our example Regex here `@([\da-z\.-]` it searches for at least a single letter character match from a-z after the @ symbol.
### Flags
In our Regex example we dont have any present *Flags* but it is an important to familiarise yourself with this important feature. A flag will help filter the input more specifically. See below the optional Javascript flags and their features:

```
i
```
- With this flag the search is case-insensitive: there is no difference between upper and lower case letters. DOG and dog would both be selected.
```
g
```
- With this flag the search looks for all matches, if this flag is not used, the result will only select the first match it finds.
```
m
```
- With this flag it use all lines to filter through, known as Multiline mode.
```
s
```
- With this flag it enables “dotall” mode, in which . matches \n, or a newline.
```
u
```
- With this flag it enables Unicode support.
```
y
```
- With this flag it enables “Sticky” mode and will searches the exact position in the text.


### Grouping and Capturing
In our Regex example;
 ```
 /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
 ```
There are three groups captured:

1. `([a-z0-9_\.-]+)`
2. `([\da-z\.-]+)`
3. `([a-z\.]{2,6})`

Capturing groups allows you to match multiple characters as single units. As shown above (as 3 seperate units, or 3 sets of parenthesis) these units will now operate in order, for example in unit 1, at least one of the characters must be present before it can go to unit 2 and so on. 

Some more examples for reference:
```
[abc]:  a, b or c
[^abc]: Not a, b or c
[a-z]:  Letters from a to z
[A-Z]:  Uppercase letters from A to Z
[0-9]:  Digits from 0 to 9 
```
### Bracket Expressions
A Regex bracket expression matches any specific set of single characters, or character class within the brackets. 
`[ ]` 

In the Regex snippet from our example indicates that we are searching for any letters between `a-z`, rather than `a`, `-`, or `z` individually.
```
[a-z\.]
```
{ }

As for curly braces they are used to specify an exact amount of characters to match. They are used after an expression, for example `\hi{2}\` will only match ‘hi’ exactly twice. 
### Greedy and Lazy Match
By default the 'greedy' quantifiers like `*` & `+`  tries to match as much of the string as possible and a the 'lazy' quantifier `?` does the opposite making it the "non-greedy" and will stop as soon as it finds a match.

### Boundaries
Regex boundaries, `\b` matches a word boundary. This will help you be able to search for singular words. While not present in our matching email regex see below will select the specific word *dog*. 
```
\bdog\b 
```
### Back-references
A *Back-reference* is a regular expression command That refers to a previous part of a matched regular expression. 
### Look-ahead and Look-behind
*Look-ahead and look-behind*, collectively known as *look-around* are used to detect for a pattern that is surrounded by another pattern. We use these to correspond to characters, it will not get the match but return with 'no match or match' and are considered as assertions. They only state whether the match is successful or not.
## Author

Created by Inspiring Web Developer and Self-Acclaimed Creative [Anastasia](https://github.com/mriya20)

[<img src="https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white"/> ](https://github.com/mriya20)
