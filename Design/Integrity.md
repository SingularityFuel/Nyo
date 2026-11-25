# Integrity

Nyo files may contain rules or type information which constrains their data.

# Built-In Types

Some basic types will exist in nyo automatically.

Having more of these makes certain common things easy to do, but as each built in type becomes a reserved keyword, it is not without cost.

| Type | Notes |
| - | - |
| text | ascii text, subject to nyo's allowed character rules |
| int | integer. can be positive, zero, or negative. unspecified bit size |
| uint | integer. positive or zero. unspecified bit size |
| num | real number |
| bool | true or false |

Also consider `func` and `ref` types for advanced uses.

# Constraints

Nyo fields can have simple constraints, like a text field having maximum length.

Complex constraints, such as a field meeting certain conditions compared to other fields, are also possible.

A nyo file is only valid when all its stated constraints are simultaneously true.