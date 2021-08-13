Regular expressions operate by moving character by character, from left to right, through a piece of text. When the regular expression finds a character that matches the first piece of the expression, it looks to find a continuous sequence of matching characters.

---

**Alternation** is performed in regular expressions with the pipe symbol, `|`, allowing us to match either the characters preceding the `|` OR the characters after the `|`.

**Grouping**, denoted with the open parenthesis `(` and the closing parenthesis `)`, lets us group parts of a regular expression together, and allows us to limit alternation to part of the regex.

---

**Character sets**, denoted by a pair of brackets `[]`, let us match *one* character from a series of characters, allowing for matches with incorrect or different spellings.

**Negated Character Sets**:  at the front of a character set, the `^` negates the set, matching any character that is *not* stated. Thus the regex `[^cat]` will match any character that is not `c`, `a`, *or* `t`, and would completely match each character `d`, `o` *or* `g`.

---

**Wildcards** `.` will match any single character (letter, number, symbol or whitespace) in a piece of text. We can use the escape character, `\`, to escape the wildcard functionality of the `.` and match an actual period.

**Ranges** allow us to specify a range of characters in which we can make a match without having to type out each individual character. The `-` character allows us to specify that we are interested in matching a range of characters.

---

**Shorthand Character Classes** represent common ranges and make writing regular expressions much simpler:

- `\w`: the “word character” class represents the regex range `[A-Za-z0-9_]`, and it matches a single uppercase character, lowercase character, digit or underscore
- `\d`: the “digit character” class represents the regex range `[0-9]`, and it matches a single digit character
- `\s`: the “whitespace character” class represents the regex range `[ \t\r\n\f\v]`, matching a single space, tab, carriage return, line break, form feed, or vertical tab

**Negated Character Classes** are shorthands that match any character not in the regular shorthand classes:

- `\W`: the “non-word character” class represents the regex range `[^A-Za-z0-9_]`, matching any character that is not included in the range represented by `\w`
- `\D`: the “non-digit character” class represents the regex range `[^0-9]`, matching any character that is not included in the range represented by `\d`
- `\S`: the “non-whitespace character” class represents the regex range `[^ \t\r\n\f\v]`, matching any character that is not included in the range represented by `\s`

---

**Fixed quantifiers**, denoted with curly braces `{}`, let us indicate the exact quantity of a character we wish to match, or allow us to provide a quantity range to match on.

- `\w{3}` will match *exactly* 3 word characters
- `\w{4,7}` will match *at minimum* 4 word characters and *at maximum* 7 word characters

An important note is that quantifiers are considered to be *greedy*. This means that they will match the greatest quantity of characters they possibly can. For example, the regex `mo{2,4}` will match the text `moooo` in the string `moooo`, and not return a match of `moo`, or `mooo`.

**Optional quantifiers**, indicated by the question mark `?`, allow us to indicate a character in a regex is optional, or can appear either `0` times or `1` time. The `?` *only* applies to the character/grouping directly before it. Use the escape character in your regex in order to match a question mark `?` in a piece of text. 

---

The **Kleene star**, denoted with the asterisk `*`, is also a quantifier, and matches the preceding character `0` or more times. This means that the character doesn’t need to appear, can appear once, or can appear many many times.

The **Kleene plus**, denoted by the plus `+` matches the preceding character `1` or more times.

The **anchors** hat `^` and dollar sign `$` are used to match text at the start and the end of a string, respectively. 

- The regex `^Monkeys: my mortal enemy$` will completely match the text `Monkeys: my mortal enemy` but not match `Spider Monkeys: my mortal enemy in the wild` 

---

### Summary:

- *Regular expressions* are special sequences of characters that describe a pattern of text that is to be matched
- We can use *literals* to match the exact characters that we desire
- *Alternation*, using the pipe symbol `|`, allows us to match the text preceding or following the `|`
- *Character sets*, denoted by a pair of brackets `[]`, let us match one character from a series of characters
- *Wildcards*, represented by the period or dot `.`, will match any single character (letter, number, symbol or whitespace)
- *Ranges* allow us to specify a range of characters in which we can make a match
- *Shorthand character classes* like `\w`, `\d` and `\s` represent the ranges representing word characters, digit characters, and whitespace characters, respectively
- *Groupings*, denoted with parentheses `()`, group parts of a regular expression together, and allows us to limit alternation to part of a regex
- *Fixed quantifiers*, represented with curly braces `{}`, let us indicate the exact quantity or a range of quantity of a character we wish to match
- *Optional quantifiers*, indicated by the question mark `?`, allow us to indicate a character in a regex is optional, or can appear either `0` times or `1` time
- The *Kleene star*, denoted with the asterisk `*`, is a quantifier that matches the preceding character `0` or more times
- The *Kleene plus*, denoted by the plus `+`, matches the preceding character `1` or more times
- The *anchor* symbols hat `^` and dollar sign `$` are used to match text at the start and end of a string, respectively