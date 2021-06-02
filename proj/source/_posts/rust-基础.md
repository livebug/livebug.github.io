---
title: Rust 基础
date: 2021-04-15 23:24:08
tags: Rust 
categories: Rust
---
# Hello,World!
## main function

```rust
fn main() {

}
```

+ a function named `main` that has no parameters and returns nothing

+ If there were parameters, they would go inside the parentheses

+ `rustfmt` to format your code ; The Rust team has included this tool with the standard Rust distribution

+ Rust style is to indent with **four spaces**, not a tab

+ `println!` calls a Rust macro

For now, you just need to know that using a `!` means that you’re calling a `macro` instead of a normal `function`.

## Compiling and Running Are Separate Steps

1. compile

    rustc main.rs

    > similar to gcc or clang   
    > After compiling successfully, Rust outputs a binary executable
2. run

    ./main  # linux

## Rust language 

Rust is an *ahead-of-time* compiled language, 
meaning you can compile a program and give the executable to someone else, and they can *run it even without having Rust installed*

## Hello,Cargo!

Cargo is Rust’s build system and package manager.

    cargo --version

## Creating a Project with Cargo

    cargo new hello_cargo

It has also initialized a new Git repository along with a `.gitignore` file.

# Cargo.toml
```toml
[package]
name = "hello-rust"
version = "0.1.0"
authors = ["aeewz"]
edition = "2018"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
```

<!-- 20210414 BEGIN -->

`[package]`  
the following statements are configuring a package

`edition = "2018"`  
the configuration information Cargo needs to `compile` your program:

- the edition of Rust to use

`[dependencies]`  
list any of your project’s dependencies  
`packages` of code are referred to as `crates`

## Building and Running a Cargo Project

- We can build a project using `cargo build`.
- We can build and run a project in one step using `cargo run`.
- We can build a project without producing a binary to check for errors using `cargo check`.
- Instead of saving the result of the build in the same directory as our code, Cargo stores it in the `target/debug` directory.

## Building for Release
When your project is finally ready for release, you can  
use `cargo build --release` to compile it with optimizations. 

This command will create an executable in `target/release` instead of `target/debug`. 

## ~ 20210415 SUMMARY 
you’ve learned how to:

+ Install the latest stable version of Rust using rustup
+ Update to a newer Rust version
+ Open locally installed documentation
+ Write and run a “Hello, world!” program using rustc directly
+ Create and run a new project using the conventions of Cargo

