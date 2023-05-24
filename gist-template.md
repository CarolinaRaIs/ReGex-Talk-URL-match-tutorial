# ReGex-Talk-URL-match-tutorial

Whether you are a beginner seeking to understand regex or an experienced developer looking to expand your skills, this tutorial will provide you with the guidance and hands-on practice needed to master URL matching using regex. 

## Summary

This tutorial provides an in-depth explanation of the regular expression ^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$ for matching and validating URLs. The regex is designed to handle a wide range of URL variations and components, including the protocol (http or https), domain/subdomain, top-level domain (TLD), and path/query parameters.

The regular expression is as follows:
/^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/

Throughout this tutorial, we will break down the regex into its individual components and explain their functionality. We will cover anchors, quantifiers, grouping constructs, character classes, and more. By the end of the tutorial, you will have a comprehensive understanding of how this regex works and how to utilize it for accurate URL matching and validation.

Please note that this regex is flexible and can handle various URL formats, including both http:// and https:// protocols, alphanumeric domain/subdomain names, TLDs consisting of 2 to 6 lowercase letters or dots, and path/query parameters containing forward slashes, alphanumeric characters, dots, hyphens, and spaces.

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

Anchors are special symbols that mark the beginning (^) and end $ of a string. In the example above, ^ denotes the start of the string, and $ indicates the end of the string.

    ^: Matches any string that starts with.
    $: Matches a string that ends with.

### Quantifiers

Quantifiers specify the quantity of characters or expressions to the left of them that must be matched. There are two types of quantifiers: greedy and lazy(?). The default behavior for quantifiers is greedy, meaning it matches to as many occurrences as possible. To make a quantifier lazy, you can append a ? after the quantifier itself; matching the minimum number of occurrences instead of the maximum.

    * and *?: The greedy quantifier that matches zero or more occurrences of the preceding character or expression.
    + and +?: Matches one or more occurrences of the preceding character or expression.
    ? and ??: Matches zero or one occurrence of the preceding character or expression.
    {n} and {n}?: Matches exactly n occurrences of the preceding character or expression.
    {n,} and {n,}?: Matches at least n occurrences of the preceding character or expression.
    {n,m} and {n,m}?: Matches from n to m occurrences of the preceding character or expression.

Examples:

    https?: The '?' makes the s optional, matching both 'https' and 'http'.

    [\da-z\.-]+: The '+' matches whats within the brackets one or more times(greedy), with the contents of the bracket containing a character class (\d) which matches a digit (0-9), as well as letters (a-z), dots (.), or hyphens (-).

    [a-z\.]{2,6}: The {2,6} matches whats within the brackets between 2 to 6 times(greedy). This indicates that there will be 2-6 copies of the sequence [a-z\.].

    [\/\w \.-]*: The '*' matches the contents within the brackets zero or more times(greedy). This means the regex will match even if there are no characters at all, or if the string contains only characters that are in the character class [\/\w \.-] In regular expressions, \w is a shorthand character class that matches any "word" character.
    
    This means \w will match:

    Any lowercase letter a-z
    Any uppercase letter A-Z
    Any digit 0-9
    The underscore character _

This means for [\/\w \.-]* there will be zero or more occurances of '/', any word character equivalent to [a-z0-9_-],'.', '-', 'www', or '//'.

    Why would the regex [\/\w \.-]* match 'www' and '//'?
    'www': Each character is a 'w', which is a lowercase letter, and thus matches the \w part of the character class.

    '//': Each character is a '/', which is specifically included in the character class as \/ (the backslash is used to escape the forward slash, indicating that we want to match the literal character '/', not use it as a regex metacharacter)

### Grouping Constructs

Grouping expressions using parentheses () helps organize and extract characters within a given group.

Examples:

    (https?:\/\/): This group allows the URL to begin with 'http://', 'https://', or none.
    ([\da-z\.-]+): This group matches one or more numbers, letters, dots, or hyphens.
    ([a-z\.]{2,6}): This group matches 2 to 6 copies of the sequence '[a-z.]'.
    ([\/\w \.-]*): This group matches multiple (greedy) occurrences (0 or more) of '/', '.', '-', 'www', or other directories.

### Bracket Expressions

Bracket expressions are used to define a character class within square brackets []. 

The example we're analyzing contains the following bracket expressions:

    [\da-z\.-]
    [a-z\.]
    [\/\w \.-]

### Character Classes

Character classes define a set of characters to match within a larger set.

Example:

    [\da-z\.-]: represents a character class that includes digits, lowercase letters, and the dot character. It can match any single character that is a digit, lowercase letter(a-z), or dot (.), or hyphens (-).

### The OR Operator

The OR operator in regular expressions is denoted by the vertical bar |. It allows you to specify alternative options to match within a pattern. It acts as a logical OR, meaning it will match either the pattern on the left side or the pattern on the right side.

Example:

    In the given regular expression ^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$:

    The OR operator is not explicitly used. However, the presence of (https?:\/\/) indicates an optional match for either http:// or https://. This achieves a similar effect as the OR operator, allowing the regular expression to handle URLs with or without a specified protocol.

### Flags

Flags in regular expressions are optional settings that can be added after the / at the end of the regular expression. They modify how the regular expression works.

Example:

    In the given regular expression /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/, no flags are specified. This means the regular expression will use the default behavior determined by the programming language or tool you are using.

    The default behavior typically performs case-sensitive matching (distinguishing between uppercase and lowercase letters), matches only the first occurrence in the input string (non-global matching), and treats each line separately (single-line matching).

If you need to change these behaviors, you can add flags after the /

Examples of commonly used flags include:

    i: Enables case-insensitive matching, allowing the regular expression to match both uppercase and lowercase characters interchangeably.

    g: Enables global matching, where the regular expression continues to search for multiple matches throughout the input string instead of stopping after the first match.

    m: Enables multi-line matching, where ^ and $ match the beginning and end of each line within a multi-line input string, instead of just the start and end of the entire string.

### Character Escapes

Character escapes in regular expressions are used to treat certain characters with special meanings as literal characters. To match these characters literally (as regular characters) instead of interpreting their special meanings, you can use the backslash \ as an escape character. When a metacharacter is preceded by a backslash, it loses its special meaning and matches the character itself.

In the given regular expression ^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$, there are a few character escapes used:

    \.: The backslash '\' escapes the metacharacter '.' dot, so it matches the character '.' literally. Without the backslash, '.' is a metacharacter that matches any character except a newline.

    \.-: In this case, '-' is not a metacharacter and does not require escaping. It matches the character '-' literally. It is used to match the literal hyphen within the character class [\da-z\.-] and [\/\w \.-]. However, if '-' is used within a character class '[ ]', it can have a special meaning. For example, [a-z] matches any lowercase letter from a to z.

    \/\/: The sequence \/ is a character escape that matches the forward slash / character itself. The purpose of this escape is to match the literal forward slashes in https://.

By using backslashes to escape metacharacters, you can match these characters literally instead of their special meaning in regular expressions.

## Author

Carolina Ramirez Islas is currently a student of University of Oregon's Coding BootCamp with a background in chemical engineering, the paper industy, and teaching. To view more of Carolina's work go to https://github.com/CarolinaRaIs or email them at determination28@gmail.com.
