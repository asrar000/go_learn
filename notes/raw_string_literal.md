# Go Raw String Literals

## Overview

A **raw string literal** in Go is a string enclosed in backticks (`` ` ``) instead of double quotes (`"`). Raw strings treat all characters literally without interpreting escape sequences, making them ideal for strings containing special characters.

## Syntax

```go
// Raw string literal
rawString := `This is a raw string`

// Regular string literal
regularString := "This is a regular string"
```

## Key Characteristics

### Raw String Literals (Backticks `` ` ``)

- ✅ No escape sequence interpretation
- ✅ Can span multiple lines
- ✅ Preserves all whitespace exactly as written
- ❌ Cannot include a backtick character
- ❌ Cannot use escape sequences like `\n` or `\t`

### Regular String Literals (Double Quotes `"`)

- ✅ Interprets escape sequences (`\n`, `\t`, `\\`, etc.)
- ✅ Can include backticks
- ❌ Cannot span multiple lines directly
- ❌ Requires escaping special characters

## Comparison Examples

### Escape Sequences

```go
// Regular string - escape sequences are interpreted
regular := "Line 1\nLine 2\tTabbed"
// Output:
// Line 1
// Line 2    Tabbed

// Raw string - escape sequences are literal
raw := `Line 1\nLine 2\tTabbed`
// Output: Line 1\nLine 2\tTabbed
```

### File Paths

```go
// Regular string - backslashes must be escaped
windowsPath := "C:\\Users\\username\\Documents\\file.txt"

// Raw string - no escaping needed
windowsPath := `C:\Users\username\Documents\file.txt`
```

### Multi-line Strings

```go
// Regular string - must use \n for newlines
regularMultiline := "Line 1\nLine 2\nLine 3"

// Raw string - natural multi-line support
rawMultiline := `Line 1
Line 2
Line 3`
```

## Common Use Cases

### 1. File Paths (Windows)

```go
path := `C:\Program Files\Go\bin\go.exe`
configPath := `D:\Projects\myapp\config\settings.json`
```

### 2. Regular Expressions

```go
// Email validation pattern
emailPattern := `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`

// Phone number pattern
phonePattern := `^\d{3}-\d{3}-\d{4}$`

// URL pattern
urlPattern := `^https?://[^\s/$.?#].[^\s]*$`
```

### 3. SQL Queries

```go
query := `
    SELECT 
        u.id,
        u.name,
        u.email,
        COUNT(o.id) as order_count
    FROM users u
    LEFT JOIN orders o ON u.id = o.user_id
    WHERE u.active = true
    GROUP BY u.id, u.name, u.email
    ORDER BY order_count DESC
    LIMIT 10
`
```

### 4. JSON Templates

```go
jsonTemplate := `{
    "name": "John Doe",
    "email": "john@example.com",
    "address": {
        "street": "123 Main St",
        "city": "Anytown",
        "zip": "12345"
    }
}`
```

### 5. HTML/XML Content

```go
htmlContent := `
<!DOCTYPE html>
<html>
<head>
    <title>My Page</title>
</head>
<body>
    <h1>Welcome</h1>
    <p>This is a paragraph with "quotes" and special characters: &, <, ></p>
</body>
</html>
`
```

### 6. Command-Line Help Text

```go
helpText := `Usage: myapp [OPTIONS] [COMMAND]

Commands:
    start       Start the application
    stop        Stop the application
    status      Check application status

Options:
    -h, --help       Show this help message
    -v, --verbose    Enable verbose output
    -c, --config     Specify config file path

Examples:
    myapp start
    myapp -v status
    myapp --config=/path/to/config.yml start
`
```

### 7. Documentation Strings

```go
const documentation = `
Package mypackage provides utilities for data processing.

This package includes:
- Data validation functions
- Data transformation utilities
- Helper functions for common operations

For more information, visit: https://github.com/user/mypackage
`
```

## Important Notes

### Whitespace Preservation

Raw strings preserve ALL whitespace, including indentation:

```go
text := `
    This line has leading spaces
        This line has more spaces
No spaces here
`
// The leading spaces and indentation are preserved exactly
```

### Cannot Include Backticks

Since backticks delimit raw strings, you cannot include them inside:

```go
// This will NOT work:
invalid := `This string has a ` backtick`

// Workaround - use a regular string or concatenation:
valid := "This string has a ` backtick"
```

### Carriage Returns

On Windows, raw strings will use the line ending from your source file (typically `\n` in most editors, but could be `\r\n`).

## Practical Example: Complete Program

```go
package main

import (
    "fmt"
    "regexp"
)

func main() {
    // Using raw string for regex pattern
    emailPattern := `^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`
    re := regexp.MustCompile(emailPattern)
    
    // Test emails
    emails := []string{
        "user@example.com",
        "invalid.email@",
        "another@valid.co.uk",
    }
    
    fmt.Println("Email Validation Results:")
    fmt.Println("========================")
    
    for _, email := range emails {
        if re.MatchString(email) {
            fmt.Printf("✓ %s is valid\n", email)
        } else {
            fmt.Printf("✗ %s is invalid\n", email)
        }
    }
    
    // Using raw string for multi-line SQL
    query := `
        SELECT name, email
        FROM users
        WHERE active = true
    `
    
    fmt.Println("\nGenerated Query:")
    fmt.Println(query)
}
```

## Best Practices

1. **Use raw strings for regex patterns** - Avoids double-escaping backslashes
2. **Use raw strings for file paths** - Especially on Windows
3. **Use raw strings for multi-line content** - SQL, JSON, HTML, etc.
4. **Be mindful of indentation** - Raw strings preserve all whitespace
5. **Use regular strings when you need escape sequences** - Like `\n`, `\t`, etc.

## Summary

| Feature | Raw String `` ` `` | Regular String `"` |
|---------|-------------------|-------------------|
| Escape sequences | Not interpreted | Interpreted |
| Multi-line | ✅ Yes | ❌ No |
| Include backticks | ❌ No | ✅ Yes |
| Whitespace | Preserved exactly | Controlled with escapes |
| Best for | Paths, regex, SQL, templates | Short strings, formatted text |

---

**Resources:**
- [Go Language Specification - String Literals](https://go.dev/ref/spec#String_literals)
- [Effective Go - Strings](https://go.dev/doc/effective_go#strings)