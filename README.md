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

> In Rust, packages of code are referred to as crates.

> Cargo expects your source files to live inside the src directory. The top-level project directory is just for README files, license information, configuration files, and anything else not related to your code. Using Cargo helps you organize your projects. There’s a place for everything, and everything is in its place.

### Compiling & Running with Cargo

`cargo build` creates an executable file in `target/debug/hello-world-rust` rather than in your current directory. Because the default build is a debug build, Cargo puts the binary in a directory named debug. You can run the executable with this command: `./target/debug/hello-world-rust`

Use `cargo run` to compile the code and then run the resulting executable all in one command.

Cargo also provides a command called `cargo check`. This command quickly checks your code to make sure it compiles but doesn’t produce an executable. Many Rustaceans run cargo check periodically as they write their program to make sure it compiles. Then they run cargo build when they’re ready to use the executable.

- We can create a project using `cargo new`.
- We can build a project using `cargo build`.
- We can build and run a project in one step using `cargo run`.
- We can build a project without producing a binary to check for errors using `cargo check`.
- Instead of saving the result of the build in the same directory as our code, Cargo stores it in the `target/debug` directory.

Note: plugin `cargo-watch` can be used to watch for changes
