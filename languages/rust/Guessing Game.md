## What is it

Simple number guessing game, to learn the basics in Rust.
## How it works

Using the rand crate, it generates a random u32 number in the range of 1 to 100 (start and end inclusive).

Inside of a loop, prompts the user for a number and compares it with the secret number to give hints

Finally, when the user guesses  (like a string), it breaks the loop and finishes.

## My own example

```rust
// Import crates (libraries)
use std::io;
use std::cmp::Ordering;
use rand::Rng;

fn main() {
	// Basic output, println!
	println!("Guess the number!");
	
	let secret_number = rand::thread_rng().gen_range(1..=100);
	
	loop {
		println!("Please input your guess.");
		
		let mut guess: String = String::new();
		
		// read_line returns a Result<Ok, Err>, if it fails
		// it breaks the program and tells the error
		io::stdin()
		.read_line(&mut guess)
		.expect("Failed to read line");
		
		// Parses the string to a u32 integer.
		let guess: u32 = match guess.trim().parse() {
			Ok(num) => num,
			Err(_) => continue
		};
		
		// cmp is a method for comparing
		// it can return three diferent values of the Ordering enum
		match guess.cmp(&secret_number) {
			Ordering::Less => println!("Too small!"),
			Ordering::Greater => println!("Too big!"),
			Ordering::Equal => {
				println!("You win!");
				break;
			}	
		}
	}
}
```

## Resources 

- https://doc.rust-lang.org/stable/book/ch02-00-guessing-game-tutorial.html
