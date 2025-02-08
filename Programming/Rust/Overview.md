# Rust Programming Language Overview

## What is Rust?
Rust is a systems programming language focused on safety, speed, and concurrency. It prevents segmentation faults and guarantees thread safety while providing powerful abstractions.

## Why Rust?
- **Memory Safety**: No null pointers, no segmentation faults, no data races.
- **Concurrency**: Fearless concurrency with ownership and borrowing.
- **Performance**: Comparable to C and C++ without a garbage collector.
- **Ecosystem**: Growing package registry (Cargo & crates.io).

## Installation
```sh
# Install Rust via rustup
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Verify installation
rustc --version
```

## Hello, World!
```rust
fn main() {
    println!("Hello, world!");
}
```

## Variables and Mutability
```rust
fn main() {
    let x = 5; // Immutable
    let mut y = 10; // Mutable
    println!("x: {}, y: {}", x, y);
    y = 20;
    println!("Updated y: {}", y);
}
```

## Ownership, Borrowing, and Lifetimes
```rust
fn main() {
    let s = String::from("Hello");
    print_string(&s); // Borrowing
    println!("String is still usable: {}", s);
}

fn print_string(s: &String) {
    println!("Borrowed: {}", s);
} // Reference goes out of scope, no move
```

## Structs and Enums
```rust
struct Person {
    name: String,
    age: u8,
}

impl Person {
    fn greet(&self) {
        println!("Hello, my name is {} and I am {} years old.", self.name, self.age);
    }
}

fn main() {
    let person = Person { name: String::from("Alice"), age: 30 };
    person.greet();
}
```

### Enums
```rust
enum Direction {
    Up,
    Down,
    Left,
    Right,
}

fn move_character(direction: Direction) {
    match direction {
        Direction::Up => println!("Moving up!"),
        Direction::Down => println!("Moving down!"),
        Direction::Left => println!("Moving left!"),
        Direction::Right => println!("Moving right!"),
    }
}

fn main() {
    move_character(Direction::Up);
}
```

## Error Handling
```rust
fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(a / b)
    }
}

fn main() {
    match divide(10.0, 2.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e),
    }
}
```

## Concurrency (Threads)
```rust
use std::thread;
use std::time::Duration;

fn main() {
    let handle = thread::spawn(|| {
        for i in 1..5 {
            println!("Spawned thread: {}", i);
            thread::sleep(Duration::from_millis(500));
        }
    });

    for i in 1..5 {
        println!("Main thread: {}", i);
        thread::sleep(Duration::from_millis(500));
    }
    
    handle.join().unwrap();
}
```

## Cargo - Rust’s Package Manager
```sh
# Create a new Rust project
cargo new my_project
cd my_project

# Build the project
cargo build

# Run the project
cargo run

# Format the code
cargo fmt

# Check for issues without compiling
cargo check
```

## Useful Rust Crates (Libraries)
- **serde** - Serialization & Deserialization
- **tokio** - Asynchronous programming
- **reqwest** - HTTP requests
- **rand** - Random number generation
- **clap** - CLI argument parsing

## Next Steps
- Explore the Rust Book: [https://doc.rust-lang.org/book/](https://doc.rust-lang.org/book/)
- Check out Rustlings: [https://github.com/rust-lang/rustlings](https://github.com/rust-lang/rustlings)
- Join the Rust community!
