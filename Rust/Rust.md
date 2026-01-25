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
		- 