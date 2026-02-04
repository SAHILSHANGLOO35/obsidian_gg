# Rust Learning Notes

## Installing Rust

If on a Linux System inside windows, run this:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Else, do the manual installation.

## Initializing a project locally

There are 2 types of projects in Rust. One are called **Binaries** and other are called **Libraries**.

- A **Binary is the final Binary** that we run i.e. ==the end user application== whereas **Library** is where we write re-usable code that our Binary(end user application) uses.
- For example - Consider end user application as Nodejs application and Library as Express framework that is already written and we use it for **building server-side web applications and APIs**.

### 1.) Start a project **(Binary)**:

```bash
cargo init
```

### 2.) Start a project (Library):

```bash
cargo init --lib
```

## What is Rust?

**Rust** is a **systems programming language** designed to be:

- **Fast** (performance like C/C++)
- **Memory-safe** (no null pointers, no data races)
- **Concurrent-friendly** (safe multithreading by default)

## Why Rust exists?

Rust was created to solve common problems in languages like C/C++:

- Segmentation faults
- Memory leaks
- Undefined behavior
- Race conditions

Rust prevents these **at compile time**, not runtime.

## Variables (nums, strings, bools)

- All variables in rust are immutable by default. To make them mutable we have to make them explicitly mutable if we want to change the values.
- `main.rs` is the entry point file of a Rust application.

## Memory Management in Rust

Whenever we run a program (C++, Rust, JS), it `allocates` and `deallocates` memory on the RAM.

![[Pasted image 20260126100127.png]]

Memory management is a crucial aspect of programming in Rust, designed to ensure safety and efficiency **without the need for a garbage collector**.

`Garbage Collector` is slow as this is a whole separate process that decides what to garbage collect and deallocate from memory and so on.

Therefore, **not having** a `garbage collector` is one of the key reasons **Rust is so fast.**

It achieves this using the:

### 1.) Mutability

### 2.) Heaps and Stack

Common way to store in memory

### 3.) Ownership model

_Ownership_ is a set of rules that govern how a Rust program manages _memory_.

In Rust, if we create data on the **heap** (like `String`), it will always have its **owner on the stack**. If that owner variable on the stack gets popped or goes out of scope, the heap data also gets removed with it.

![[Pasted image 20260126171807.png]]

Now if we make another variable in Stack pointing to the same data in the Heap then Rust says original variable becomes invalid and now the new variable is the owner of the data in the Heap.

Now, taking ==Rihanna== as an example: Rihanna wants to be with one boyfriend at a time. If her boyfriend dies, she also dies. But if, before her boyfriend is about to die, she commits to another guy, then she will survive and also get a new boyfriend.

_This is Ownership and memory safety in Rust._

### 4.) Borrowing and references

We can transfer `ownerships` of variables to fns. By passing a **reference** of the string to the function `take_ownership`, the ownership of of the string remains with the original variable, in the `main` function. This allows us to use that variable again after the function call.

**==Rules==**:

1. We can have multiple mutable references of a variable.
2. If we have one mutable reference then we can't have any other immutable or mutable references.

Code snippet of ==Borrowing Variable==:

**Mutable references**

```rust
let mut s1: String = String::from("Hello");
let s2: &mut String = &mut s1;
// update_word(&mut s1); // Cannot be borrowed by the
// update_word function as it is already a 
// reference once in the above line {s2}

println!("{}", s1);
println!("{}", s2);

fn update_word() {}
```

### 5.) Lifetimes

## Structs

Structs let us structure data together like we do in c++.

```rust
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
    println!("{} {} is {} years old.", user.first_name, user.last_name, user.age);
}
```

- Structs are similar to **Objects** in [[Javascript]]
- The closer comparison between structs in Javascript and Rust is that - ==structs in rust are actually more closer to classes in Javascript as classes have methods, static methods associated with them.==

We can implement methods/functions to struct also i.e. we can attach a method to that struct, so that when someone defines a struct of that particular type, then that they will also get access to that function also as shown:

```rust
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

Here the `(&self)` argument in the function area of `impl Rect` ==refers to the current struct i.e. on which particular struct we are calling the area function on.== This is called _**member function**_.

## Enums

Enums let us **enumerate** over various types of a value.

For example - Shapes, Directions etc.

```rust
enum Shape {
    Rectangle,
    Circle
}

fn print_area(shape: Shape) {
    println!("Hi There!")
}
```

### Enums with values

In the above `enum` example we just declared the enums without having any values for them like `height` and `width` or `radius`.

For example - Declaring enums of type shape with values associated with them:

```rust
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
    println!("The are of rectangle is: {:.2}", calculate_area(rectangle));
    
    let square = Shape::Square(20.0);
    println!("The area of square is: {:.2}", calculate_area(square));
    
    let circle = Shape::Circle(10.0);
    println!("The area of circle is: {:.2}", calculate_area(circle));
}
```

### Default Enums by Rust - (Options/Result)

The ==Option enum== lets us return either **Some** value or **None** value.

The option enum was introduced in Rust to handle the concept of nullability in a safe and expressive way.

Rust doesn't have null.

```rust
pub enum Option<T> {
    None,
    Some(T)
}
```

### Error handling using Result

Different languages have different ways to handle error.

JavaScript, for example, has the concept of `try-catch` block.

Example using Code snippet - The `example.txt` does not exists, therefore the function without panicking or without throwing any error prints us the error statement without any error in the code just like `try-catch` in JS.

```rust
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

## Collections

Rust's standard library includes a number of very useful data structures called **collections**.

Most data types represents one specific value, but collections can contain multiple values, the data these collections point to is **stored on the heap**.

### 1.) Vectors

Vectors allow us to store more than one value in a single data structure that puts all the values next to each other in memory.

```rust
fn main() {
    let mut vec = Vec::new();
    vec.push(1);
    vec.push(2);
    vec.push(3);
    
    println!("{:?}", vec);
}
```

Initializing using ==Rust macros== - This `vec!` will create a fresh vector first and then pushes these values into it.

```rust
fn main() {
    let numbers = vec![1, 2, 3];
    for i in numbers {
        println!("{}", i);
    }
}
```

### 2.) Hashmaps

Hashmaps store a key-value pair in Rust. Similar to objects in JS, Dict in Python and Hashmaps in Java, Maps in C++.

```rust
let mut users: HashMap<String, u32> = HashMap::new();
users.insert(String::from("Sahil"), 22);
users.insert(String::from("Karan"), 21);
```

## Iterators

`.iter()` method -> ==immutable iterator== -> immutable reference for iterating over the values via an iterator.

The `iter()` method in Rust provides a way to iterate over the elements of a collection by **borrowing** them.

`.iter()`, `.iter_mut()` basically returns us an **iterator**. And all iterators have `.next()`.

```rust
fn main() {
    let mut v1 = vec![1, 2, 3];
    
    for val in v1_iter {
        println!("{}", val);
    }
}
```

`.iter_mut` method -> ==mutable iterator== -> mutable reference to mutate values via an iterator.

```rust
fn main() {
    let mut v1 = vec![1, 2, 3];
    let v1_iter = v1.iter_mut(); // Type IterMut
    
    for val in v1_iter {
        *val = *val + 1;
    }
    
    println!("{:?}", v1);
}
```

`.next()` -> To call the .next(), the iterator itself must be mutable.

`.next()` takes a mutable reference to the iterator and returns an `Option<Item>`

So, What must be **mutable**?

- ❌ NOT the collection
- ❌ NOT the values
- ✅ **The iterator variable**

`.intoIter()` -> Used to convert a collection into an iterator that takes _**ownership**_ of the collection.

**Useful when:**

1. We no longer need the original collection.
2. When we need to squeeze performance benefits by transferring ownership (avoiding references).

![[Pasted image 20260128095935.png]]

**Iterators** also give us some benefits like some methods (eg-.sum(), map()).

- Some methods are called as **Consuming Adapters** eg - `sum()` - (a function that ends up consuming the iterators i.e. taking up the ownership by that `sum fn`).
- Others are called as **Iterator Adapters** eg - `map()` - (are methods defined on the Iterator Trait that don't consume the iterator. Instead, they ==produce different iterators== by changing some aspect of the original iterator.)

### `.collect()`

is used to convert the iterator back to vector.

```rust
let v1_filter: Vec<i32> = v1_iter.filter(|x| *x % 2 != 0).map(|x| x * 2).collect();
```

## Strings vs Slices

The `String` type which is provided by Rust's standard library rather than coded into the core language, is a:

- growable,
- mutable,
- owned, and
- UTF-8 encoded string type.

`Slices` let us reference a contiguous sequence of elements in a collection rather than the whole collection.

A `slice` is a kind of reference, so it does not have ==ownership==.

## Generics

One `fn` definition but two different uses.

```rust
fn largest<T: std::cmp::PartialOrd>(a: T, b: T) -> T {
    if a > b { a } else { b }
}

fn main() {
    let bigger_number = largest(3, 7);
    let bigger_char = largest('a', 'd');
}
```

## Traits: Defining Shared Behavior

A _**trait**_ defines the functionality a particular type has and can share with other types. We can use traits to define shared behavior in an abstract way. We can use _**trait bounds**_ to specify that a generic type can be any type that has certain behavior.

**NOTE:** Traits are similar to a feature often called _**interfaces**_ in other languages, although with some differences.

**Steps:**

### 1.) Defining the trait:

```rust
pub trait Summary {
    fn summarize(&self) -> String;
}
```

### 2.) Defining the struct:

```rust
struct User {
    name: String,
    age: u32,
}
```

### 3.) Implementing a Trait on the struct

```rust
impl Summary for User {
    fn summarize(&self) -> String {
        return format!("User {} is {} years old", self.name, self.age);
    }
}

fn main() {
    let user = User {
        name: String::from("Karan Singh"),
        age: 27,
    }
    
    println!("{}", user.summarize());
}
```

==Question== - Why do we need structs with references to have a lifetime parameter?

So we know how long the `struct` can live.

## Generic Type Parameters, Trait Bounds, and Lifetimes Together

```rust
fn longest_with_an_announcement<'a, T>(x: &'a str, y: &'a str, ann: T) -> &'a str
where T: Display,
{
    println!("Announcement! {ann}");
    if x.len() > y.len() {
        return x;
    } else {
        return y;
    }
}

fn main() {
    let str1 = String::from("small");
    let str2 = String::from("longer");
    let ann: String = String::from("Announcing the longest string");
    let result = longest_with_an_announcement(&str1, &str2, ann);
    println!("Longest string is: {}", result);
}
```

## Multithreading

Although Rust is multithreaded, but we need to explicitly spawn extra threads.

```rust
fn main() {
    thread::spawn(|| {
        let mut c = 0;
        for i in 0..500 {
            c = c + 1;
        }
    });
}
```

## Moving Variable to spawned thread

This is done so that the spawned thread takes up the ownership of the variable as the thread may continue even after the main ends and then that variable have no existence.

## Message Passing from one thread to another

We drop this transmitter variable because we don't want the below receiver to wait for the transmitter to send some data, only the producers are sending data.

```rust
fn main() {
    let (tx, rx) = mpsc::channel();
    for i in 0..10 {
        let producer = tx.clone();
        thread::spawn(move || {
            let mut sum: u64 = 0;
            for j in i * 10_000_000..((i + 1) * 10_000_000) {
                sum = sum + j;
            }
            producer.send(sum).unwrap();
        });
    }
    drop(tx); // -> We drop this transmitter varible 
    // because we don't want the below receiver to wait for the
    // transmitter to send some data, only the producers are sending
    // data.
    
    let mut final_sum = 0;
    for val in rx {
        final_sum = final_sum + val;
    }
    println!("{final_sum}");
}
```

## Macros

Macros are code that write other code. This is called `metaprogramming`.

So when we write `println!` which is a macro, then this line of code gets expanded to a lot of lines of code, this similar thing happens when we create vector like the below one.

```rust
let v = vec![1, 2, 3];
```

## Annotations & Decorators

