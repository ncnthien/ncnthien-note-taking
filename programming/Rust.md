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