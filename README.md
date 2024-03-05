# Understanding Email Matching Regex

This tutorial will explain a regular expression (regex) used to validate email addresses. The regex we will be discussing is: `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`

## Summary

This regex is used to validate email addresses. It checks if the input string follows the general pattern of an email address, which is `username@domain.extension`. The username can contain lowercase letters, numbers, underscores, dots, and hyphens. The domain can contain digits, lowercase letters, dots, and hyphens. The extension can contain lowercase letters and dots, and must be between 2 to 6 characters long.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)

## Regex Components

### Anchors

The `^` and `$` are anchors which denote the start and end of the line respectively. This means the match must start at the beginning of the line and end at the end of the line.

In the context of regular expressions, anchors are special characters that specify the position of the pattern in relation to a line of text. They do not match any character themselves, but rather the position before, after, or between characters.

The `^` symbol is known as the start of line anchor. When used at the beginning of a regular expression, it asserts that the following pattern must start at the beginning of the line. For example, the regex `^abc` will match any line that starts with "abc".

The `$` symbol is known as the end of line anchor. When used at the end of a regular expression, it asserts that the preceding pattern must be at the end of the line. For example, the regex `abc$` will match any line that ends with "abc".

When used together, as in `^abc$`, the regular expression will match an entire line that consists only of "abc". Any additional characters at the start or end of the line would result in no match.

It's important to note that the behavior of these anchors can be affected by the multiline mode of the regex engine. In multiline mode, `^` and `$` match the start and end of each line, rather than the start and end of the entire input string.

Code:
```javascript
let regex = /^abc$/;
console.log(regex.test("abc")); // true
console.log(regex.test("abcd")); // false
console.log(regex.test("abcdabc")); // false
console.log(regex.test("abcabc")); // false 
```

### Quantifiers

The `+` is a quantifier that means one or more of the preceding element. The `{2,6}` is a quantifier that means between 2 and 6 of the preceding element.

Quantifiers in regular expressions define how many instances of the preceding element are required for a match. They are used to specify the amount of repetition.

The `+` quantifier means "one or more" of the preceding element. It requires that the preceding character, group, or character class exists at least once for a match to occur. For example, in the regex `a+`, it will match "a", "aa", "aaa", and so on, but not an empty string.

The `{n,m}` quantifier means "between n and m" of the preceding element, where n and m are integers. This quantifier is used when you want to specify a specific range of repetitions. For example, in the regex `a{2,6}`, it will match "aa", "aaa", "aaaa", "aaaaa", "aaaaaa", but not "a" or "aaaaaaa".

It's important to note that quantifiers are greedy by default, meaning they will match as many instances of the preceding element as possible. For example, in the string "aaaaa", the regex `a+` will match the entire string, not just the first "a". However, this behavior can be modified with certain flags or additional quantifiers.

### Character Classes

The character classes used are `[a-z0-9_\.-]`, `[\da-z\.-]`, and `[a-z\.]`. They match a range of characters that can be used in the email address.

Character classes in regular expressions are denoted by square brackets `[]` and they match any one character enclosed within them. They are used when you want to match one of many characters.

In the context of the email matching regex, three character classes are used:

1. `[a-z0-9_\.-]`: This character class matches any one lowercase letter (a-z), digit (0-9), underscore (_), dot (.), or hyphen (-). This is used to match the username part of the email address, which can contain any of these characters.

2. `[\da-z\.-]`: This character class matches any one digit (\d is a shorthand character class that matches any digit), lowercase letter (a-z), dot (.), or hyphen (-). This is used to match the domain part of the email address, which can contain any of these characters.

3. `[a-z\.]`: This character class matches any one lowercase letter (a-z) or dot (.). This is used to match the extension part of the email address, which can contain any of these characters.

It's important to note that the dot and hyphen are escaped with a backslash. This is because in the context of a character class, the dot does not need to be escaped, but the hyphen does when it's not used to specify a range. To avoid confusion, it's a common practice to escape both of them.

### Grouping and Capturing

The `()` are used for grouping and capturing. They group the regex into three parts: the username, domain, and extension.

Grouping and capturing are powerful features in regular expressions that allow you to group together parts of your pattern, which can then be treated as a single unit. This is done using parentheses `()`.

#### Grouping

Grouping is useful when you want to apply a quantifier to multiple characters. For example, in the regex `(ab)+`, the `+` quantifier applies to the entire group `ab`, not just the character `b`. This regex will match "ab", "abab", "ababab", etc.

In the context of the email matching regex, grouping is used to separate the email address into three parts: the username, domain, and extension. This is done by surrounding each part with parentheses, like so: `([a-z0-9_\.-]+)`, `([\da-z\.-]+)`, and `([a-z\.]{2,6})`.

#### Capturing

In addition to grouping, parentheses also create a capturing group. A capturing group "captures" the part of the string matched by the part of the regex inside the parentheses. These captured groups can then be referred back to with backreferences (using `\1`, `\2`, etc.).

In the email matching regex, there are three capturing groups corresponding to the username, domain, and extension of the email address. However, this regex does not use backreferences, so the capturing feature is not utilized in this case.

It's important to note that not all parentheses create capturing groups. If you want to group without capturing, you can use non-capturing parentheses, which are written as `(?:...)`.

### Bracket Expressions

This regex uses bracket expressions to specify the range of characters that can be used in the email address.

Bracket expressions, also known as character classes, are a feature of regular expressions that allow you to match any one character out of a set of characters. They are denoted by square brackets `[]`.

Inside a bracket expression, you can specify individual characters or a range of characters. For example, `[abc]` will match any one of "a", "b", or "c". `[a-z]` will match any one lowercase letter from "a" to "z".

In the context of the email matching regex, bracket expressions are used to specify the range of characters that can be used in different parts of the email address:

- `([a-z0-9_\.-]+)`: The bracket expression `[a-z0-9_\.-]` specifies that the username part of the email address can contain any one lowercase letter (a-z), digit (0-9), underscore (_), dot (.), or hyphen (-).
- `([\da-z\.-]+)`: The bracket expression `[\da-z\.-]` specifies that the domain part of the email address can contain any one digit (\d is a shorthand character class that matches any digit), lowercase letter (a-z), dot (.), or hyphen (-).
- `([a-z\.]{2,6})`: The bracket expression `[a-z\.]` specifies that the extension part of the email address can contain any one lowercase letter (a-z) or dot (.).

It's important to note that inside a bracket expression, most special characters lose their special meaning and represent themselves. For example, the dot (.) usually matches any character, but inside a bracket expression, it just represents a dot. However, some characters like the hyphen (-) can have a special meaning inside a bracket expression (to specify a range), so they need to be escaped with a backslash if they are meant to represent themselves.

### Greedy and Lazy Match

This regex uses greedy match, which tries to match as much as possible.

In the context of regular expressions, "greedy" and "lazy" are terms used to describe the matching behavior of quantifiers.

#### Greedy Match

By default, quantifiers in regular expressions are "greedy". This means they will try to match as much as possible. For example, given the string "aaaaa" and the regex `a+`, the `+` quantifier is greedy, so it will match the entire string, not just the first "a".

The greedy behavior is due to the way the regex engine works. It starts at the beginning of the string and tries to match the entire pattern at that position. If it can't, it moves to the next position and tries again. This continues until a match is found or the end of the string is reached.

In the context of the email matching regex, the `+` and `{2,6}` quantifiers are greedy. This means they will try to match as many characters as possible, while still allowing the entire regex to match.

#### Lazy Match

In contrast, a "lazy" or "non-greedy" quantifier will try to match as little as possible. This is achieved by appending a `?` after the quantifier. For example, the regex `a+?` will match one "a" in the string "aaaaa", not the entire string.

Lazy quantifiers are useful when you want to match the smallest possible part of the string that satisfies the pattern. However, they are not used in the email matching regex, so all quantifiers in this regex are greedy.

## Author

This tutorial was written by [Shelby Hutchinson](https://github.com/shhutc18). Feel free to reach out with any questions.
