## Welcome to Rust 1.0

# Preface

There are N number of tutorials out there for learning Rust, but the Holy Book is only 1 🫡 - [**The Rust Lang Book**](https://doc.rust-lang.org/book)

Throughout this series, we'll dive through this book and learn every concept in rust comprehensively by building cool projects 😎, so that you can flex it on your portfolio!

This series will place application-based learning on a level playing field with theoretical learning and I'll try to explain the concepts clearly in the best by building insignificant but helpful projects

*Let's jump right on to learning* 🚀

# Why learn Rust?

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664463771416/f1Hi8PLor.png align="center")
*Rust is the most loved language for the past 7 years!*

Besides this stat, Rust has got superpowers built-in. Not every developer wants to write **low-level code** that will ruin their brains for bad memory management and safety! Rust breaks down these barriers by eliminating the old traps and providing a friendly, polished set of tools to help you along the way. 

Rust can be used in any domain, literally! From core systems dev to create a new blockchain to building web apps, anything can be built using rust's powers. You can even load rust into embedded systems and build some crazy ass robotics projects.

- Rust has an inbuilt state of art compiler that avoids any type of bugs in the code. Even beginners with 0 low-level language experience can understand what the error/warning is and focus more on coding the logic rather than hunting down bugs xD
- Also, Rust's dependency manager and build tool Cargo, makes development way easier and simplifies the developer experience!

# Installing Rust

## Linux or macOS

Installation link - https://www.rust-lang.org/tools/install

Paste this command in your terminal to install **Rustup**
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Now, restart your current shell to reload your PATH env.

> For Windows, the process is the same but you will also need to install [MSVC build tools](https://visualstudio.microsoft.com/downloads/?q=build+tools) for Visual Studio 2013 or later.

## Verify your installation

```sh
$ rustc --version

rustc 1.64.0 (a55dd71d5 2022-09-19)
```

# Let's do HELLO WORLD!

Now that you have successfully installed rust on your machine, let's get started with the universal **Hello, World** program. 

Create a directory `hello_world` and `cd` into it.

```sh
$ mkdir hello_world
$ cd hello_world
```

Inside this, create a new file `main.rs` (.rs is the file extension for rust) and open the file in your favorite code editor

```rust
fn main() {
    println!("Hello, World!");
}
```
Don't worry about the syntax, just paste this code in there. Now open the terminal in this folder and then build this file.

```sh
rustc main.rs
```
This will compile the rust file into an executable which we will run!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1664469276088/xZ-pZLsMR.png align="left")

Congratulations 🥳 We successfully ran our first program in rust!

# Conclusion
Hope you learned something new today! Feel free to drop your questions in the comments below 😄 

In the next blog, we'll break this hello world program and understand what is happening under the hood and how rust works!

## Useful Links

- [twitter/sahilpabale](https://twitter.com/SahilPabale/)

- [linkedin/sahilpabale](https://www.linkedin.com/in/sahil-pabale/)

- [✉️ email me](mailto:dev.sahilpabale@gmail.com)