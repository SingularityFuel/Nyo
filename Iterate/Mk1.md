# Overview

1. This is a specification for files with extension '.nyo'
2. Nyo files may contain only a subset of ASCII: newline, space, capital and lowercase letters, digits, and the following 32special characters: { } [ ] ( ) \ / ' ` " ~ < > ? ! @ # $ % ^ & * _ - + = | : ; , .
3. Nyo files always contain an even number (possibly zero) of the double-quote character "
4. Regular Text refers to any part of a nyo file which is before the first double-quote, after the last double-quote, or between an even-numbered double-quote and the next double-quote in the file. Excludes the double-quotes themselves.
5. Quoted Text refers to any part of a nyo file which is between an odd-numbered double-quote and the next double-quote in the file. Excludes the double-quotes themselves.
6. When the backslash character appears inside quoted text, it must either be followed by N, T, S, or Q. These pairs of characters starting with a backslash are called Escaped Newlines, Escaped Tabs, Escaped Backslashes, and Escaped Doublequotes.
7. Each nyo file is composed of zero or more Statements separated by Statement Separators. A Statement Separator is defined as any semicolon or newline in regular text. A Statement is defined as either all characters before the first Statement Separator, all characters after the last Statement Separator, or the characters between one Statement Separator and the next. Statements exclude the separators themselves. Statements can be empty, such as the Statement between two consecutive newlines. Quoted Text contains no Statement Separators by definition.