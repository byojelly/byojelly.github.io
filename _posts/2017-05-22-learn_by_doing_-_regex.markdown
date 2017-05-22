---
layout: post
title:  Learn By Doing - Regex
date:   2017-05-22 13:22:26 -0400
---


Regular Expressions, also referred to by many as Regex,  is a powerful tool used by developers to match and manipulate text patterns (strings) within your programming.  

How do you create a Regex in your code?  The most common implementation of Regex in Ruby is using /..../ to encapsulate your query at the end of a line of code (please note that ... represents content for the Regex). 

Examples of Regex include:
*    /\w+\s\w+/
*    /d+/

Now lets breakdown both of these examples
/\w+\s\w+/
The above Regex will look for strings that have 2 words.  Specifically, \w+ means that we are going to look for 1 or more word characters, with \s which indicates a space, along with \w+ one or more word characters.

/d+/
This Regex indicates that it will be looking for a range of digits. d+ indicates that it will be looking for 1 or more digit characters which will be 0 - 9. 

When creating Metacharacters it is important keep the following in mind:
1. Metacharacters
2. Bracket expressions
3. Quantifiers
4. Anchors

Metacharacters - Metacharacters have a specific meaning when appearing in a pattern. To match them literally they must be backslash-escaped. 
* /./ - Any character except a newline.
* /./m - Any character (the m modifier enables multiline mode)
* /\w/ - A word character ([a-zA-Z0-9_])
* /\W/ - A non-word character ([^a-zA-Z0-9_])
* /\d/ - A digit character ([0-9])
* /\D/ - A non-digit character ([^0-9])
* /\h/ - A hexdigit character ([0-9a-fA-F])
* /\H/ - A non-hexdigit character ([^0-9a-fA-F])
* /\s/ - A whitespace character: /[ \t\r\n\f]/
* /\S/ - A non-whitespace character: /[^ \t\r\n\f]/
* 
Bracket expressions - The bracket expression \p{} construct matches characters with the named property.
* /\p{Alnum}/ - Alphabetic and numeric character
* /\p{Alpha}/ - Alphabetic character
* /\p{Blank}/ - Space or tab
* /\p{Cntrl}/ - Control character
* /\p{Digit}/ - Digit
* /\p{Graph}/ - Non-blank character (excludes spaces, control characters, and similar)
* /\p{Lower}/ - Lowercase alphabetical character
* /\p{Print}/ - Like \p{Graph}, but includes the space character
* /\p{Punct}/ - Punctuation character
* /\p{Space}/ - Whitespace character ([:blank:], newline, carriage return, etc.)
* /\p{Upper}/ - Uppercase alphabetical
* /\p{XDigit}/ - Digit allowed in a hexadecimal number (i.e., 0-9a-fA-F)
* /\p{Word}/ - A member of one of the following Unicode general category Letter, Mark, Number, Connector_Punctuation
* /\p{ASCII}/ - A character in the ASCII character set
* /\p{Any}/ - Any Unicode character (including unassigned characters)
* /\p{Assigned}/ - An assigned character

Quantifiers -  Repetition metacharacter specify how many times a specific Metacharacter needs to occur. Such metacharacters are called quantifiers.
* * - Zero or more times
* + - One or more times
* ? - Zero or one times (optional)
* {n} - Exactly n times
* {n,} - n or more times
* {,m} - m or less timest

Quantifiers side note - Repetition is greedy by default: as many occurrences as possible are matched while still allowing the overall match to succeed. By contrast, lazy matching makes the minimal amount of matches necessary for overall success. A greedy metacharacter can be made lazy by following it with ?.

Anchors - Anchors are metacharacters that match the zero-width positions between characters, anchoring the match to a specific position.
* ^ - Matches beginning of line
* $ - Matches end of line
* \A - Matches beginning of string.
* \Z - Matches end of string. If string ends with a newline, it matches just before newline
* \z - Matches end of string
* \G - Matches point where last match finished
* \b - Matches word boundaries when outside brackets; backspace (0x08) when inside brackets
* \B - Matches non-word boundaries
* (?=pat) - Positive lookahead assertion: ensures that the following characters match pat, but doesn't include those characters in the matched text
* (?!pat) - Negative lookahead assertion: ensures that the following characters do not match pat, but doesn't include those characters in the matched text
* (?<=pat) - Positive lookbehind assertion: ensures that the preceding characters match pat, but doesn't include those characters in the matched text
* (?<!pat) - Negative lookbehind assertion: ensures that the preceding characters do not match pat, but doesn't include those characters in the matched text

-----------------------------------------------------------------------------------------------------------------------------------------------------
Although Regexs are a poweful tool, it is difficult to master. Many programmers I have spoken to say it is a very difficult topic to teach and that it is easier to learn through hands on practice.  A friend of mine provided me with a Regex simulator which has helped me immensly. 

http://www.regexr.com/

Tutorial = https://youtu.be/fOH62XXGdLs

This link provides you with an interactive screen to practice your code against text while also providing very handy tools to help you refine your code. RegExr provides real-time visual results, syntax highlighting, tooltips, and undo/redo (Ctrl-Z / Y) so it's easy and fun to explore Regular Expressions.  Give it a try and see for yourself!



