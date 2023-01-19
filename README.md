# Learning Rust

## Hello World

Make a file `main.rs`.

```rust
fn main() {
    println!("Hello, world!");
}
```

### Compiling & Running

Before running a program, you need to compile it: run `rustc main.rs`

Now, in the directory you have the source code file with the `.rs` extension, the executable file, `main`. From here you run main with `./main`

> Rust is an ahead-of-time compiled language, meaning you can compile a program and give the executable to someone else, and they can run it even without having Rust installed.

## Cargo

Cargo is Rust’s build system and package manager.

Create a new project: `cargo new hello-world-rust`

> Cargo expects your source files to live inside the src directory. The top-level project directory is just for README files, license information, configuration files, and anything else not related to your code. Using Cargo helps you organize your projects. There’s a place for everything, and everything is in its place.

### Compiling & Running with Cargo

`cargo build` creates an executable file in `target/debug/hello-world-rust` rather than in your current directory. Because the default build is a debug build, Cargo puts the binary in a directory named debug. You can run the executable with this command: `./target/debug/hello-world-rust`

Use `cargo run` to compile the code and then run the resulting executable all in one command.

Cargo also provides a command called `cargo check`. This command quickly checks your code to make sure it compiles but doesn’t produce an executable. Many Rustaceans run `cargo check` periodically as they write their program to make sure it compiles. Then they run cargo build when they’re ready to use the executable.

- We can create a project using `cargo new`.
- We can build a project using `cargo build`.
- We can build and run a project in one step using `cargo run`.
- We can build a project without producing a binary to check for errors using `cargo check`.
- Instead of saving the result of the build in the same directory as our code, Cargo stores it in the `target/debug` directory.

**Note:** plugin `cargo-watch` can be used to watch for changes

### Crates

> In Rust, packages of code are referred to as crates:
> [crates.io](crates registry) is where people in the Rust ecosystem share their open source Rust projects.

Run `cargo update` to explicitly update the versions of dependencies.

Running the `cargo doc --open` command will build documentation provided by all of your dependencies locally and open it in your browser.

## Common Programming Concepts in Rust

### Constants !== Variables

Variables are immutable by default `let x = 6`, but can be made mutable by declaring `let mut x = 6`. Variables can only be used in functions.

Constants are **always** immutable. The type _must_ be annotated. Constants can be declared in any scope, including the global scope, which makes them useful for values that many parts of code need to know about. The last difference is that constants may be set only to a constant expression, not the result of a value that could only be computed at runtime like `const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;`. Rust’s naming convention for constants is to use all uppercase with underscores between words.

### Shadowing

Helpfully Rust allows us to shadow the previous value of guess with a new one. **Shadowing** lets us reuse the variable name rather than forcing us to create two unique variables, such as guess_str and guess for example. This feature is often used when you want to convert a value from one type to another type.

> Rustaceans say that the first variable is shadowed by the second, which means that the second variable is what the compiler will see when you use the name of the variable. In effect, the second variable overshadows the first, taking any uses of the variable name to itself until either it itself is shadowed or the scope ends. ex:

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }

    println!("The value of x is: {x}");
}
```

```bash
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/variables`
The value of x in the inner scope is: 12
The value of x is: 6

```

#### DO THIS ✅

```rust
    let spaces = "   ";
    let spaces = spaces.len();
```

#### NOT THAT ❌

```rust
   let mut spaces = "   ";
   spaces = spaces.len();
```

### Data Types

_Rust is a statically typed language._

#### Scalar Types

##### Integer Types

| Length  | Signed | Unsigned |
| ------- | ------ | -------- |
| 8-bit   | i8     | u8       |
| 16-bit  | i16    | u16      |
| 32-bit  | i32    | u32      |
| 64-bit  | i64    | u64      |
| 128-bit | i128   | u128     |
| arch    | isize  | usize    |

Signed and unsigned refer to whether it’s possible for the number to be negative, whether the number needs to have a sign with it (signed) or whether it will only ever be positive and can therefore be represented without a sign (unsigned).

##### More Types

`f32` and `f64` are the two floating point types. The default type is `f64` because on modern CPUs it’s roughly the same speed as `f32` but is capable of more precision.

`bool` is a single byte in size, with two possible values: `true` and `false`.

`char` type is the language’s most primitive alphabetic type. Specify `char` literals with single quotes, as opposed to string literals, which use double quotes. Rust’s `char` type is four bytes in size and represents a Unicode Scalar Value, which means it can represent a lot more than just ASCII.

#### Compound Types

##### Tuples

Tuples have a fixed length: once declared, they cannot grow or shrink in size. To access the parts of a tuple, use destructuring, or access it using `.`

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    // use .
    let five_hundred = x.0;

    let six_point_four = x.1;

    let one = x.2;

    // destructuring
    let (a, b, c) = x;
}
```

##### Arrays

Every element of an array must have the same type. Unlike arrays in some other languages, arrays in Rust have a fixed length.

> Arrays are useful when you want your data allocated on the stack rather than the heap or when you want to ensure you always have a fixed number of elements. An array isn’t as flexible as the vector type, though. A vector is a similar collection type provided by the standard library that is allowed to grow or shrink in size. If you’re unsure whether to use an array or a vector, chances are you should use a vector. However, arrays are more useful when you know the number of elements will not need to change.

You write an array’s type using square brackets with the type of each element, a semicolon, and then the number of elements in the array, like so:

```rust
let months = ["January", "February", "March", "April", "May", "June", "July",
              "August", "September", "October", "November", "December"];
let a: [i32; 5] = [1, 2, 3, 4, 5];
```
