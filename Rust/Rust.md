- ## Installing Rust
	- If on a Linux System inside windows, run this -
		- `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`
		- Else, do the manual installation.
- ## Initializing a project locally
	- There are 2 types of projects in Rust. One are called **Binaries** and other are called **Libraries**.
	- A **Binary is the final Binary** that we run i.e. ==the end user application== whereas **Library** is where we write re-usable code that our Binary(end user application) uses.
	- For example - Consider end user application as Nodejs application and Library as Express framework that is already written and we use it for **building server-side web applications and APIs**.
		- 1.) Start a project **(Binary)**:
			- `cargo init`
		- 2.) Start a project (Library):
			- `cargo init --lib`
- ## What is Rust ?
	- **Rust** is a **systems programming language** designed to be:
		- **Fast** (performance like C/C++)
		- **Memory-safe** (no null pointers, no data races)
		- **Concurrent-friendly** (safe multithreading by default)
- ## Why Rust exists ?
	- Rust was created to solve common problems in languages like C/C++:
		- Segmentation faults
		- Memory leaks
		- Undefined behavior
		- Race conditions
	- Rust prevents these **at compile time**, not runtime.
- ## Variables (nums, strings, bools)
	- All variables in rust are immutable by default. To make them mutable we have to make them explicitly mutable if we want to change the values.
	- `main.rs` is the entry point file of a Rust application. 
	- This is the code snippet to **check whether a number is even or not** -
		- ```
			  fn main() {
				  println!("{}", is_even(20));
			  }
			  
			  fn is_even(num: i32) -> bool {
				  if num % 2 == 0 {
					  return true;
				  }
				  return false;
			  }
		  ```
- ## Memory Management in Rust
	- Whenever we run a program (C++, Rust, JS), it `allocates` and `deallocates` memory on the RAM.
	- ![[Pasted image 20260126100127.png]]
	  - Memory management is a crucial aspect of programming in Rust, designed to ensure safety and efficiency **without the need for a garbage collector**.
	  - `Garbage Collector` is slow as this is a whole separate process that decides what to garbage collect and deallocate from memory and so on.
	  - Therefore, **not having** a `garbage collector` is one of the key reasons **Rust is so fast.**
	  - It achieves this using the -
		  - **1.)** **Mutability**
		  - **2.)** **Heaps and Stack** --> common way to store in memory
		  - **3.)** **Ownership model** --> *Ownership* is a set of rules that govern how a Rust program manages *memory*.
			  - In Rust, if we create data on the **heap** (like `String`), it will always have its **owner on the stack**. If that owner variable on the stack gets popped or goes out of scope, the heap data also gets removed with it.
			  - ![[Pasted image 20260126171807.png]]
			  - Now if we make another variable in Stack pointing to the same data in the Heap then Rust says original variable becomes invalid and now the new variable is the owner of the data in the Heap.
			  - Now, taking ==Rihanna== as an example: Rihanna wants to be with one boyfriend at a time. If her boyfriend dies, she also dies. But if, before her boyfriend is about to die, she commits to another guy, then she will survive and also get a new boyfriend.
			  - *This is Ownership and memory safety in Rust.*
		  - **4.)** **Borrowing and references**
			  - We can transfer `ownerships` of variables to fns. By passing a **reference** of the string to the function `take_ownership`, the ownership of of the string remains with the original variable, in the `main` function. This allows us to use that variable again after the function call.
			  - Code snippet of ==Borrowing Variable==:
				  - ```
					    fn main() {
						    let my_string = String::from("Hello World");
						    borrow_variable(&my_string); // Pass a reference
						    // to `my_string`
						    println!("{}", my_string);
					    }
					    
					    fn borrow_variable(some_string: &String) {
						    println!("{}", some_string); // `some_string` is
						    borrowed and not moved.
					    }
				    ```
			-  **Mutable references**
				- ```
					  let mut s1: String = String::from("Hello");
					  let s2: &mut String = &mut s1;
					  // update_word(&mut s1); // Cannot be borrowed by the
					  update_word function as it is already a 
					  reference once in the above line {s2}
					  
					  println!("{}", s1);
					  println!("{}", s2);
					  
					  fn update_word() {}
				  ```
		  - 5.) **Lifetimes**
- ## Structs
	- Structs let us structure data together like we do in c++.
	- ```
		  struct User {
			  active: bool,
			  username: String,
			  email: String,
			  sign_in_count: u64,
		  }
		  
		  fn main() {
			  let user: User = User {
				  first_name: String::from("Sahil"),
				  last_name: String::from("Shangloo"),
				  age: 22,
			  };
			  println!("{} {} is {} years old.", user.first_name,
			  user.last_name,user.age);
		  }
	  ```
	- Structs are similar to **Objects** in [[Javascript]]
	- The closer comparison between structs in Javascript and Rust is that - ==structs in rust are actually more closer to classes in Javascript as classes have methods, static methods associated with them.==
	- We can implement methods/functions to struct also i.e. we can attach a method to that struct, so that when someone defines a struct of that particular type, then that they will also get access to that function also as shown -
		- ```
			  struct Rect {
				  width: u32,
				  height: u32
			  }
			  
			  impl Rect {
				  fn area(&self) -> u32 {
					  self.width * self.height
				  }
			  }
		  ```
	- Here the `(&self)` argument in the function area of `impl Rect` ==refers to the current struct i.e. on which particular struct we are calling the area function on.==
- ## Enums
	- Enums let us **enumerate** over various types of a value.
	- For example - Shapes, Directions etc.
		- ```
			  enum Shape {
				  Rectangle,
				  Circle
			  }
			  
			  fn print_area(shape: Shape) {
				  println!("Hi There!")
			  }
		  ```
	- ## Enums with values
		- In the above `enum` example we just declared the enums without having any values for them like `height` and `width` or `radius`.
		- For example - Declaring enums of type shape with values associated with them -
		- ```
			  enum Shape {
				  Rectangle(f64, f64),
				  Square(f64),
				  Circle(f64)
			  }
			  
			  fn calculate_area(shape: Shape) -> f64 {
				  // pattern matching
				  match shape {
					  Shape::Rectangle(l, b) => l*b,
					  Shape::Square(s) => s*s,
					  Shape::Circle(r) => PI*r*r,
				  }
			  }
			  
			  fn main() {
				  let rectangle = Shape::Rectangle(20.0, 10.0);
				  println!("The are of rectangle is: {:.2}",
				  calculate_area(rectangle));
				  
				  let square = Shape::Square(20.0);
				  println!("The area of square is: {:.2}, 
				  calculate_area(square));
				  
				  let circle = Shape::Circle(10.0);
				  println!("The area of circle is: {:.2}",
				  calculate_area(circle));
			  }
		  ```
	- ## Default Enums by Rust - (Options/Result)
		- The ==Option enum== lets us return either **Some** value or **None** value.
		- The option enum was introduced in Rust to handle the concept of nullability in a safe and expressive way.
		- Rust doesn't have null.
		-  ```
			  pub enum Option<T> {
				  None,
				  Some(T)
			  }
		  ```
	- ## Error handling using Result
		- Different languages have different ways to handle error.
		- JavaScript, for example, has the concept of `try-catch` block.
		- Example using Code snippet - The `example.txt` does not exists, therefore the function without panicking or without throwing any error prints us the error statement without any error in the code just like `try-catch` in JS.
			- ```
				  fn main() {
					  let res = fs::read_to_string("example.txt");
					  match res {
						  Ok(content) => {
							  println!("File content: {}", content);
						  }
						  Err(err) => {
				            println!("Error: {}", err);
			            }
					}
				}
			  ```
- ## New topic