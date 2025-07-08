# JxLang 0.3.126
<a href="README.md">简体中文</a> | English<br><br>
A lightweight, custom programming language designed for simplicity and interactive scripting. Built on top of Python, `jxlang` offers a REPL environment and supports basic programming constructs such as variables, loops, functions, and library imports. 

JxLang is based on a multi-layered language architecture—like a virtual machine within a virtual machine—making it a fun tool for experimentation and learning. However, due to its design, JxLang is intended purely for entertainment and casual tinkering, and is **not** suitable for production or real-world project development.

## Installation

Install by PyPI
```bash
pip install jxlang
```

## Update Content
<ul>
<li>Added flexible dynamic struct functionality</li>
<li>Enhanced multi-line input display with improved formatting</li>
<li>Fixed variable type display issues</li>
</ul>

## Features

- **Single-Line Comments**: `#` stands for single-line comments.
- **Variable Declaration**: Use `let` to declare variables.
- **Loops**: `for` loops with range-based iteration.
- **I/O Operations**: `enter()` for input, `say()` for output.
- **Library Imports**: Import Python libraries via `cite` with optional aliases.
- **List/Table Structures**: Create and manipulate lists (`table(...)`).
- **Function Support**: Define and call custom functions.
- **Multi-line Input**: Support for multi-line code input in REPL with improved formatting.
- **Dynamic Structs**: Create and manipulate flexible data structures.
- **Type Inspection**: Use `shape()` to inspect variable types.
- **Exit Session**: `endend()` for exiting current session.
- **REPL Support**: Interactive shell for quick testing.

## Quick Examples

### 1. Variable Declaration and Printing
```python
let x: 5
say(x + 3)  # Output: 8
# You can use double quotation marks or single quotation marks when assigning strings to variable names
let a: "hello"
say(a)      # hello
let a: 'world'
say(a)      # world
```

### 2. Loop
```python
(i -> 1 && 5).for(
    say(i)
    )
# Output: 1 2 3 4 5
```

### 3. Function Definition and Calling
```python
func(x && y -> add):
    out x + y

say(add(5 && 3))  # Output: 8

# Multi-line function definition
func(x && y -> calculate):
    let temp: x * 2
    out temp + y

say(calculate(3 && 4))  # Output: 10
```

### 4. Input and Output
```python
let name: enter()  # User enters "Alice"
say("Hello, " + name)  # Output: Hello, Alice
```

### 5. Import Python Libraries with Aliases
```python
cite math as m
say(m.sqrt(25))  # Output: 5.0

cite numpy as np
let a: np.array([1,2,3])
say(a)          # Output: [1,2,3]

# Import specific module with alias
cite pandas as pd
let df: pd.DataFrame({'A': [1,2,3]})
say(df)         # Output: DataFrame with column A

# Data visualization with matplotlib
cite matplotlib.pyplot as plt
let x: np.linspace(0, 10, 100)
let y: np.sin(x)
plt.plot(x, y)
plt.title("Sine Wave")
plt.show()      # Displays the plot
```
<p>* JxLang can call Python Libraries only if they are installed in your Python environment.</p>

### 6. List and Table Operations
```python
let lst: table(1, 2, 3)
say(lst[0])       # Output: 1
say(lst)          # Output: [1,2,3]

let tbl: table(1, 2; 3, 4)
say(tbl)          # Output: [[1, 2], [3, 4]]

# List manipulation
push 1 -> lst     # Add 1 to the end of the list
say(lst)          # [1,2,3,1]

push tbl -> lst
say(lst)          # [1,2,3,1,[[1,2],[3,4]]]

out 1 -> lst      # Remove first occurrence of 1 and store in outlist
say(lst)          # [2,3,[[1,2],[3,4]]]
say(lst.outlist)  # [1,1]

throw 2 -> lst    # Permanently remove 2 from the list
say(lst)          # [3,[[1,2],[3,4]]]

let lst[0]: 2     # Replace element at index 0 with 2
say(lst)          # [2,[[1,2],[3,4]]]
```
<p>* JxLang creates n+1 dimensional lists using n semicolons as separators.</p>

### 7. Dynamic Structs and Type Inspection
```python
# Define a struct
struct Person {
    name: string,
    age: int,
    address: string
}

# Create a struct instance
let person: Person {
    name: "John",
    age: 30,
    address: "New York"
}

# Create nested struct
struct Info {
    info: Person
}

let i: Info {
    info: Person {
        name: "John",
        age: 30,
        address: "New York"
    }
}

# Access struct members
say(person->name)      # Output: John
say(person->age)       # Output: 30
say(i->info->name)     # Output: John
say(i->info->age)      # Output: 30

# Dynamically modify struct values
let person->name: 'Mike'
let person->age: 40
say(person->name)     # Output: Mike
say(person->age)      # Output: 40
```

### 8. Type Checking
```python
let a: 100
let b: 'Alice'
let c: table(1,2,3)

func (i -> add):
    out i

# Display types
shape(a)    # Output: int
shape(b)    # Output: string
shape(c)    # Output: list
shape(add)  # Output: function

# Other types can be checked using the shape method in the same way
```

## Using the REPL

Start the interactive environment by running:
```bash
jxlang
```

Example REPL session with multi-line input:
```
jxlang> func(x && y -> add):
    ... out x + y
jxlang> say(add(5 && 3))
8
jxlang> endend(0)  # you can use numbers from 0 to 9 for endend()
Exiting with code 0
```

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request.  
For major changes, open an issue first to discuss your ideas.

## License

This project is licensed under the Apache License.

---

Happy coding! 🚀
