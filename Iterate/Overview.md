# Overview

1. This is a specification for files with extension '.nyo'
    - File-system metadata, transport wrappers, and EOF indicators are not part of the content defined by this specification.
2. **Nyo Files** may contain only a subset of ASCII: newline, space, capital and lowercase letters, digits, and the following 32 special characters: { } [ ] ( ) \ / ' ` " ~ < > ? ! @ # $ % ^ & * _ - + = | : ; , .
    - In this specification, “character” means one of the allowed ASCII characters listed above.
3. **Nyo Files** always contain an even number (possibly zero) of the double-quote character "
4. **Unquoted Text** refers to any part of a **Nyo File** which is before the first double-quote, after the last double-quote, or between an even-numbered double-quote and the next double-quote in the file. Excludes the double-quotes themselves. If a **Nyo File** has zero double-quote characters, its entire contents are **Unquoted Text**.
5. **Quoted Text** refers to any part of a **Nyo File** which is between an odd-numbered double-quote and the next double-quote in the file. Excludes the double-quotes themselves. All characters allowed in **Nyo Files** except the double quote itself may appear inside **Quoted Text**.
    - By definition, every character in a **Nyo File** including whitespace is either a double-quote character, part of **Unquoted Text**, or part of **Quoted Text**.
6. The backslash character can only appear inside **Quoted Text**. When it appears, it must either be followed by N, T, S, or Q. These pairs of characters starting with a backslash are called **Escaped Newlines**, **Escaped Tabs**, **Escaped Backslashes**, and **Escaped Doublequotes**.
    - These sequences are always treated as two characters as written in the file, not the single characters they represent, by the rules in this specification.
7. Each **Nyo File** is composed of one or more **Statements** separated by **Statement Separators**. A **Statement Separator** is defined as any semicolon or newline in **Unquoted Text**. A **Statement** is defined as either all characters before the first **Statement Separator**, all characters after the last **Statement Separator**, or the characters between one **Statement Separator** and the next. **Statements** exclude the **Statement Separators** themselves. **Statements** can be empty, such as the **Statement** between two consecutive newlines. **Quoted Text** contains no **Statement Separators** by definition. A **Nyo File** containing zero **Statement Separators** is interpreted as a file with one **Statement**, which may be the empty **Statement**.
8. Each **Statement** is composed of zero or more **Tokens** which may be separated by **Token Separators**. **Quoted Text** including its initial and final double-quotes is always one **Token**. A single space or any number of consecutive spaces create a single **Token Separator**. Some consecutive **Tokens** do not require **Token Separators** and will therefore not have spaces between them, but each space in **Unquoted Text** is part of a **Token Separator**. **Statement Separators** are neither **Tokens** nor **Token Separators** by definition, since they exist outside **Statements**. There is no such thing as an empty **Token**. Leading and trailing **Token Separators** in a **Statement** are ignored.
    - A zero-length **Quoted Text** segment is still a **Token**. A zero-length region of **Unquoted Text** (created by a closing quote immediately followed by an opening quote) contains no **Tokens**.
9. The special characters ' ` $ @ # can only appear inside **Quoted Text**.
10. **Tokens** in **Unquoted Text** may contain only capital and lowercase letters, digits, and the following 27 special characters: { } [ ] ( ) / ~ < > ? ! @ # $ % ^ & * _ - + = | : , .
    - The characters { } [ ] ( ) always form single-character **Tokens**. **Statements** containing these **Grouping Tokens** always contain an even number of them arranged in such a way that each **Group** opened is always subsequently closed, and any **Group** opened inside another **Group** is always closed before that other **Group** closes.
    - The & and | characters always form single-character **Tokens**. These **Tokens** are the **AND Operator** and **OR Operator**. Note that Nyo does not use the conventional two-character versions of these operators which appear in other languages.
    - The _ character can only appear as the single-character **Null**.
    - The - character can only appear as the single-character **Minus Operator**.
    - The + character can only appear as the single-character **Plus Operator**.
    - The * character can only appear as the single-character **Multiply Operator**.
    - The / character can only appear as the single-character **Divide Operator**.
    - The ! character can appear as the single-character **NOT Operator** or as part of the two-character **ELSE** ( !? ) **Token**. Note that the **NOT Operator** will have more valid usages than it does in most programming languages.
    - The % character can only appear as the single-character **Modulo Operator**.
    - The ^ character can only appear as the single-character **Exponentiate Operator**.
    - The > and < characters can only appear as the single-character **Lesser** and **Greater** operators. Note the absence of dedicated LTE or GTE operators.
    - The = character can only appear as the single-character **Equal** operator.
    - The ? character can appear either as the single-character **IF** **Token** or as part of the two-character **THEN** ( ?: ) or **ELSE** ( !? ) **Tokens**. When a ? character is preceded by !, the larger token is always formed rather than **IF**. When a ? character is followed by :, the larger token is always formed rather than **IF**. The sequence !?: never appears.
    - The : character can appear as the single-character **Assign Operator** or as part of the **THEN** ( ?: ) **Token**.
    - The ~ character always appears as the single-character **Like Operator**.
    - The . character, when not directly between digit characters, is the single-character **Dot Token**.
    - The , character is always the single-character **Comma Token**.
11. Outside of **Quoted Text**, letters and digits exist only in three types of **Tokens**: **Names**, **Keywords**, and **Numbers**.
    - **Names** begin with a letter and are followed by any uninterrupted series of letters and digits. A **Name** ends when any other character appears.
    - **Keywords** contain only letters and have special effects defined by the Nyo specification in advance.
    - **Numbers** are composed of one or more digits and at most one decimal point. The decimal point is neither the first nor the last character in the **Number**. The first digit in a **Number** can only be zero if that zero is immediately followed by a decimal or if the **Number** is the zero character on its own. A **Number** ends when any non-digit character (except a correctly placed decimal) appears.
12. The end of a **Nyo File** terminates any **Tokens** or **Statements**.
13. A **Nyo File** which does not or cannot meet this full specification is invalid in its entirety.