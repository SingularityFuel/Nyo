# Files

- Nyo will use files with the `.nyo` extension
- File format will be strict rather than permissive whenever possible.
- Files must contain only allowed characters
- Allowed characters will be a subset of ASCII
- Similar to JSON, a file is implied to be a single object. However, the outermost braces {} can be omitted.

| Allowed Characters | Notes |
| --- | --- |
| A-Z and a-z | Names |
| 0-9 | Numbers and Names (except first character) |
| {} | used to make objects |
| space, newline | separate items but are otherwise ignored outside of literals |
| " | creates strings |
| \\ | escape character within strings |
| ; | equivalent to newline |
| , | equivalent to space |
| : | for key:value and ternary (if) operator |
| ? | used in ternary (if) operator or to ask for input inside $ |
| / \* . ^ + - % | can make numbers |
| & ! > < ( ) = | grouping and operations |
| \| | OR operation |
| $ | variable substitution |
| \_ | null |
| \[ \] | indicate a data type within |
| \# | begins comment until next newline |
| @ | indicates pointer type |
| \` ' \~ | only in strings |
