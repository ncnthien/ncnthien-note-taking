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
# Using Structs to Structure Related Data
- Use `struct` to define a struct
```rust
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}
```
- Create an *instance* to use struct
```rust
fn main() {
    let user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };
}
```
- Use dot notation to get a specific value from a struct
```rust
fn main() {
    let mut user1 = User {
        active: true,
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");
}
```
- Return a struct in function
```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username: username,
        email: email,
        sign_in_count: 1,
    }
}
```
### Using the Field Init Shorthand
```rust
fn build_user(email: String, username: String) -> User {
    User {
        active: true,
        username,
        email,
        sign_in_count: 1,
    }
}
```
### Creating Instances from Other Instances with Struct Update Syntax
- Use `..` syntax to create a new instance from the old one
```rust
fn main() {
    // --snip--

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```
### Using Tuple Structs Without Named Fields to Create Different Types
```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```
### Unit-Like Structs Without Any Fields
```rust
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```
## An Example Program Using Structs
```rust
fn main() {
    let width1 = 30;
    let height1 = 50;

    println!(
        "The area of the rectangle is {} square pixels.",
        area(width1, height1)
    );
}

fn area(width: u32, height: u32) -> u32 {
    width * height
}
```
### Refactoring with Tuples
- Refactor the code above
```rust
fn main() {
    let rect1 = (30, 50);

    println!(
        "The area of the rectangle is {} square pixels.",
        area(rect1)
    );
}

fn area(dimensions: (u32, u32)) -> u32 {
    dimensions.0 * dimensions.1
}
```
### Refactoring with Structs: Adding More Meaning
```rust
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        area(&rect1)
    );
}

fn area(rectangle: &Rectangle) -> u32 {
    rectangle.width * rectangle.height
}
```
### Adding Useful Functionality with Derived Traits
- To for some structs, adding the outer attribute `#[derive(Debug)]` just before the struct definition
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!("rect1 is {:?}", rect1);
}
```
- Another way to print out a value using the `Debug` format is to use the `dbg! marco`
- An example where we're interested in the value that gets assigned to the `width` field, as well as the value of the whole struct in `rect1`:
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let scale = 2;
    let rect1 = Rectangle {
        width: dbg!(30 * scale),
        height: 50,
    };

    dbg!(&rect1);
}
```
## Method Syntax
### Defining Methods
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```
- We can also choose to give a method the same name as one of the struct's fields
```rust
impl Rectangle {
    fn width(&self) -> bool {
        self.width > 0
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    if rect1.width() {
        println!("The rectangle has a nonzero width; it is {}", rect1.width);
    }
}
```
### Methods with More Parameters
```rust
fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

	impl Rectangle {
	    fn area(&self) -> u32 {
	        self.width * self.height
	    }

	    fn can_hold(&self, other: &Rectangle) -> bool {
	        self.width > other.width && self.height > other.height
	    }
	}

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```
- Methods can take multiple parameters that we add to the signature after the `self` parameter, and those parameters work just like parameters in functions
### Associated Functions
- All functions defined within an `impl` block are called *associated functions* because they're associated with the type named after the `impl`
- We can defined associated functions that don't have `self` as their first parameter (and thus as not methods)
- Associated functions that aren't methods are often used for constructors that will return a new instance of the struct
```rust
impl Rectangle {
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}
```
- The `self` keywords in the return type and in the body of the function are aliases for the type that appears after the `impl` keyword, which in this case is `Rectangle`
- Use `::` syntax to call this function
```rust
let sq = Rectangle::square(3);
```
- `::` is used for both associated functions and namespaces created by modules
### Multiple `impl` Blocks
```rust
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```
- There's no reason to separate these methods into multiple `impl` blocks here, but this is valid syntax
# Enums and Pattern Matching
## Defining an Enum
- Enums give you a way of saying a value is one of a possible set of values
```rust
enum IpAddrKind {
    V4,
    V6,
}
```
### Enum Values
- Create instance using value of enum
```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```
- Define a function that takes any `IpAddrKind`
```rust
fn route(ip_kind: IpAddrKind) {}
```
- Put the data directly into each enum variant
```rust
enum IpAddr {
	V4(String),
	V6(String),
}

let home = IpAddr::V4(String::from("127.0.0.1"));

let loopback = IpAddr::V6(String::from("::1"));
```
- Or we can have different type also
```rust
enum IpAddr {
	V4(u8, u8, u8, u8),
	V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);

let loopback = IpAddr::V6(String::from("::1"));
```
### The `Option` Enum and Its Advantages Over Null Values
```rust
enum Option<T> {
    None,
    Some(T),
}
```
- You can use `None` and `Some` directly without the `Option::` prefix
- You have to convert an `Option<T>` to a `T` before you can perform `T` operations with it
- This helps catch one of the most common issues with null: assuming that something isn't null when it actually is
## The match Control Flow Construct
- `match` is like `switch` in other languages
- Use `match` with `enum`
```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```
### Patterns That Bind to Values
```rust
#[derive(Debug)] // so we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        }
    }
}
```
### Matching with `Option<T>`
- Handle `Option<T>` using `match`
```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		None => None,
		Some(i) => Some(i + 1),
	}
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```
### Matches Are Exhaustive
```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
	match x {
		Some(i) => Some(i + 1),
	}
}
```
- This piece of code will cause a bug
### Catch-all Patterns and the _ Placeholder
- Catch all other possibilities using `other`
```rust
let dice_roll = 9;
match dice_roll {
	3 => add_fancy_hat(),
	7 => remove_fancy_hat(),
	other => move_player(other),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn move_player(num_spaces: u8) {}
```
- Want a catch-all but don't want to use the value in the catch-all, use `_`
```rust
let dice_roll = 9;
match dice_roll {
	3 => add_fancy_hat(),
	7 => remove_fancy_hat(),
	_ => reroll(),
}

fn add_fancy_hat() {}
fn remove_fancy_hat() {}
fn reroll() {}
```
## Concise Control Flow with `if let`
```rust
let config_max = Some(3u8);
match config_max {
	Some(max) => println!("The maximum is configured to be {}", max),
	_ => (),
}
```
- Write in a shorter way using `if let`
```rust
let config_max = Some(3u8);
if let Some(max) = config_max {
	println!("The maximum is configured to be {}", max);
}
```
- Using `if let` means less typing, less indentation, less boilerplate, but losing the exhaustive checking that `match` enforces
- Use `if let` and `else`
```rust
let mut count = 0;
if let Coin::Quarter(state) = coin {
	println!("State quarter from {:?}!", state);
} else {
	count += 1;
}
```
# Managing Growing Projects with Packages, Crates, and Modules
- **Packages:** A Cargo feature that lets you build, test, and share crates
- **Crates:** A tree of modules that produces a library or executable
- **Modules** and **use:** Let you control the organization. scope, and privacy of paths
- **Paths:** A way of naming an item, such as a struct, function, or module
## Packages and Crates
- A *crate* is the smallest amount of code that the Rust compiler considers at a time
- Crates can contain modules, and the modules may be  defined in other files that get compiled with the crate
- A *crate* can come in one of two forms: a binary crate or a library crate
- *Binary crates* are programs you can compile to an executable that you can run, such as a command-line program or a server, each must have a function called `main` that defines what happens when the executable runs
- *Library crates* don't have a `main` function, an they don't compile to an executable, they define functionality intended to be shared with multiple projects
- *Crate root* is a source file that the Rust compiler starts from and makes up the root module of your crate
- A *package* is a bundle of one or more crates that provides a set of functionality, containing a *Cargo.toml* file that describes how to build those crates
- Cargo is actually a package that contains the binary crate for the command-line tool, also contains a library crate that the binary crate depends on.
## Defining Modules to Control Scope and Privacy
### Modules Cheat Sheet
- **Start from the crate root:** When compiling a crate, the compiler first looks in the crate root file (usually *src/lib.rs* for a library crate or *src/main.rs* for a binary crate) for code to compile
- **Declaring modules:** In the crate root file, you can declare new modules; say, you declare a "garden" module with `mod garden;`. The compiler will look for the module's code in these places:
	- Inline, within curly brackets that replace the semicolon following `mod garden`
	- In the file *src/garden.rs*
	- In the file *src/garden/mod.rs*
- **Declaring submodules:** In any other than the crate root, you can declare submodules. For example, you might declare `mod vegetables;` in *src/garden.rs.* The compiler will look for the submodule's code within the directory named for the parent module in these places:
	- Inline, directly following `mod vegetables`, within curly brackets instead of the semicolon
	- In the file *src/garden/vegetables.rs*
	- In the file *src/garden/vegetables/mode.rs*
- **Paths to code in modules:** Once a module is part of your crate, you can refer to code in that module from anywhere else in that same crate, as long as the privacy rules allow, using the path to the code. For example, an `Asparagus` type in the garden vegetables module would be found at `crate::garden::vegetables::Asparagus`.
- **Private vs public:** Code within a module is private from its parent modules by default. To make a module public, declare it with `pub mod` instead of `mod`. To make items within a public module public as well, use `pub` before their declarations
- **The `use` keyword:** Within a scope, the `use` keyword creates shortcuts to items to reduce repetition of long paths. In any scope that can refer to `crate::garden::vegetables::Asparagus`, you can create a shortcut with `use crate::garden::vegetables::Asparagus;` and from then on you only need to write `Asparagus` to make use of that type in the scope
- Creating a crate named `backyard` illustrating above rules.
```
backyard
├── Cargo.lock
├── Cargo.toml
└── src
    ├── garden
    │   └── vegetables.rs
    ├── garden.rs
    └── main.rs
```
- The crate root file is *src/main.rs*
```rust
use crate::garden::vegetables::Asparagus;

pub mod garden;

fn main() {
    let plant = Asparagus {};
    println!("I'm growing {:?}!", plant);
}
```
- The `pub mod garden;` line tells the compiler to include the code it find in *src/garden.rs*, which is:
- Filename: src/garden.rs
```rust
pub mod vegetables;
```
- Here, `pub mod vegerables;` means the code in *src/garden/vegetables.rs* is included too. That code is:
```rust
#[derive(Debug)]
pub struct Asparagus {}
```
# Common Collections
- Often used collections in Rust:
	- A *vector* allows to store a variable number of values next to each other
	- A *string* is a collection of characters
	- A *hash map* allows to associate a value with a particular key
## Storing Lists of Values with Vectors
- Vectors allow to store more than one value in a single data structure that puts all the values next to each other in memory
- Vectors can only store values of the same type
### Creating a New Vector
- Create a new empty vector
```rust
let v: Vec<i32> = Vec::new();
```
- Or can use `vec!`
```rust
let v = vec![1, 2, 3];
```
### Updating a Vector
- Create a vector and add elements to it
```rust
let mut v = Vec::new();

v.push(5);
v.push(6);
v.push(7);
v.push(8);
```
### Reading Elements of Vectors
```rust
let v = vec![1, 2, 3, 4, 5];

let third: &i32 = &v[2];
println!("The third element is {third}");

let third: Option<&i32> = v.get(2);
match third {
	Some(third) => println!("The third element is {third}"),
	None => println!("There is no third element."),
}
```
- If use `get` instead of `[ ]`, you will give the type `Option<&T>` that we can use with `match`
### Iterating over the Values in a Vector
- Use `for` loop
```rust
let v = vec![100, 32, 57];
for i in &v {
	println!("{i}");
}
```
- Or use `mut` to mutate during the loop
```rust
let mut v = vec![100, 32, 57];
for i in &mut v {
	*i += 50;
}
```
### Using an Enum to Store Multiple Types
```rust
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }

    let row = vec![
        SpreadsheetCell::Int(3),
        SpreadsheetCell::Text(String::from("blue")),
        SpreadsheetCell::Float(10.12),
    ];
```
### Dropping a Vector Drops Its Elements
```rust
    {
        let v = vec![1, 2, 3, 4];

        // do stuff with v
    } // <- v goes out of scope and is freed here
```
