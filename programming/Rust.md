---
tags: programming-language
---
# Common Programming Concepts
## Variables and Mutability
- Variables are immutable by default
- Assign a new value for a variable
```rust
let x = 5;
```
- Use `let mut` for mutable variables
```rust
let mut x = 5;
```
### Constants
- Cannot use `mut` with constants
- Declare constants using `const`
- Type of the value *must* be annotated
```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```
### Shadowing
- Be able to declare a new variable with the same name as a previous variable
```rust
fn main() {
	let x = 5;

	let x = x + 1;

	{
		let x = x * 2;
		println!("The vlaue of x in the inner scope is: {x}");
	}

	println!("The value of x is: {x}");
}
```
- The difference between shadowing and `mut` is:
	- Be able to perform a few transformations on a value but have the variable be immutable after those transformations have been completed
	- Creating a new variable when using the `let` keyword again, be able to change the type of the value but reuse the same name
## Data Types
- There're two data type subsets: **scalar and compound**
### Scalar Types
- A *scalar* type presents a single value
- There're four scalar types: integers, floating-point numbers, Booleans, characters
#### Integer Types
- singed integer types start with `i`
- singed integer types start with `u`

| Length | Signed | Unsigned |
|--------|--------|-----------|
|8\-bit|`i8`|`u8`|
|16\-bit|`i16`|`u16`|
|32\-bit|`i32`|`u32`|
|64\-bit|`i64`|`u64`|
|128\-bit|`i128`|`u128`|
|arch|`isize`|`usize`|
- signed is for negative numbers
- unsigned is for positive numbers
- signed variant can store numbers from -(2<sup>n-1</sup>) to 2<sup>n-1</sup> -1
- unsigned variant can store numbers from 0 to 2<sup>n</sup> - 1
#### Floating-Point Types
- There're are two primitive types for *floating-numbers*: `f32` and `f64`
```rust
fn main() {
	let x = 2.0; // f64
	let y: f32 = 3.0; // f32
}
```
#### Numeric Operations
```rust
fn main() {
	// addition
	let sum = 5 + 10;

	// subtraction
	let difference = 95.5 - 4.3;
	
	// multiplication
	let product = 4 * 30;
	
	// division 
	let quotient = 56.7 / 32.2;
	let truncated = -5 / 3; // Results in -1
	
	// remainder
	let remainder = 43 % 5;
}
```
#### The Boolean Type
```rust
fn main() {
	let t = true;
	let f: bool = false; // with explicit type annotation 
}
```
#### The Character Type
```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // with explicit type annotation
    let heart_eyed_cat = '😻';
}
```
### Compound Types
- There're two primitive compound types: *tuples* and *arrays*
#### The Tuple Type
- Tuples have a fixed length: once declared, they cannot grow or shrink in size
```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```
- To get the individual values out of a tuple, use pattern matching to destructure a tuple value
```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The value of y is: {y}");
}
```
- To access a tuple element, use (`.`)
```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;
}
```
#### The Array Type
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
    let a: [i32; 5] = [1, 2, 3, 4, 5]; // type i32, size = 5
    let a = [3;5] // a = [3, 3, 3, 3, 3]
}
```

##### Accessing Array Elements
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```
## Functions
- Rust uses *snake case* as the conventional style for function and variable names
```rust
fn main() {
    println!("Hello, world!");

    another_function();
}

fn another_function() {
    println!("Another function.");
}
```
### Parameters
```rust
fn main() {
    another_function(5);
}

fn another_function(x: i32) {
    println!("The value of x is: {x}");
}
```
### Statements and Expressions
- Function bodies are made up of a series of statements optionally ending in an expression
- **Statements** are instructions that perform some action and do not return a value
- **Expressions** evaluate to a resultant value
```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    }; // this expression return 4 -> y = 4

    println!("The value of y is: {y}");
}
```
### Functions with Return Values
```rust
fn five() -> i32 {
    5
}

fn main() {
    let x = five();

    println!("The value of x is: {x}");
}
```
## Comments
```rust
fn main() {
	// I’m feeling lucky today
    let lucky_number = 7; // I’m feeling lucky today
}
```
## Control Flow
### `if` Expressions
```rust
fn main() {
    let number = 3;

    if number < 5 {
        println!("condition was true");
    } else {
        println!("condition was false");
    }
}
```
#### Handling Multiple Conditions with `else if`
```rust
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```
#### Using `if` in a `let` Statement
```rust
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```
### Repetition with Loops
- There're three kinds of loops: `loop`, `while`, and `for`
#### Repeating Code with `loop`
```rust
fn main() {
	// Infinite loop
    loop {
        println!("again!");
    }
}
```
#### Returning Values from Loops
- Use `break` to return a value from loop
```rust
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```
#### Loop Labels to Disambiguate Between Multiple Loops
- Specify `loop label` on a loop, then use with `break` or `continue` to specify that those keywords apply to the labeled loop instead of the innermost loop
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```
#### Conditional Loops with `while`
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```
#### Looping through a collection with `for`
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];
    let mut index = 0;

    while index < 5 {
        println!("the value is: {}", a[index]);

        index += 1;
    }
}
```
- or you can use `for..in`
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```
- or you can use `Range` with `rev()` function to reverse the `Range`
```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```
