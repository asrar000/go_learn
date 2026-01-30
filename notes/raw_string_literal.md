# Raw String Literals in Go

## What is a Raw String Literal?

A **raw string literal** in Go is a string enclosed using **backticks**:

``


Raw string literals represent text **exactly as written**, without interpreting escape sequences.

---

## Syntax

```go
s := `Hello World`
Defined using backticks (`)

No escaping or processing is done

Raw vs Interpreted String Literals
Go supports two types of string literals.

Interpreted String Literal (Double Quotes)
s := "Hello\nWorld"
Characteristics
Escape sequences are processed

\n → newline

\t → tab

\" → double quote

Output
Hello
World
Raw String Literal (Backticks)
s := `Hello\nWorld`
Characteristics
Escape sequences are NOT processed

\n is treated as literal text

Text is preserved exactly

Output
Hello\nWorld
Multiline Strings
Raw string literals can span multiple lines without using \n.

query := `
SELECT id, name
FROM users
WHERE active = true;
`
This is one of the biggest advantages of raw strings.

Allowed in Raw String Literals
Multiline text

Double quotes (")

Tabs and spaces as-is

Newlines as written

s := `He said "Hello"`
Not Allowed in Raw String Literals
Escape sequences (\n, \t, etc.)

String interpolation

Backticks inside the string

s := `Line1\nLine2` // \n remains literal
Invalid example:

s := `This is invalid ` string`
Common Use Cases
Raw string literals are commonly used for:

SQL queries

JSON / XML data

Regular expressions

Multiline text

Windows file paths

path := `C:\Users\Asrar\Documents`
When NOT to Use Raw String Literals
When escape sequences are required

When formatting with \n or \t is needed

When backticks must be included in the string

Summary Table
Feature	Interpreted String (" ")	Raw String (` `)
Escape sequences	Yes	No
Multiline support	No	Yes
Exact text preservation	No	Yes
Key Takeaways
Raw string literals use backticks

They preserve text exactly as written

Ideal for multiline and formatted text

No escape sequence processing