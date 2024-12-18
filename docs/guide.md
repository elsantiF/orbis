# Orbis

Orbis will be a new-gen language, it will prioritize human readability while ensuring computational efficiency. It will be:

- Native compiled (initially to x86 and ARM)
- Modern
- Adaptable learning curve
- Based on the DRY (Don't Repeat Yourself) principle
- Fast to iterate

## Inspiration

Every human creation is inspired by others, and Orbis draws inspiration from several programming languages:

- C/C++
- Rust
- Zig
- Nim
- Odin
- Go/V
- C#
- Kotlin/Scala
- Elixir/Gleam
- TypeScript

Yes, that is a lot of languages, and some were left out. Orbis will learn the lessons from them.

## Goals

1. A language that can be applied in a, but not limited to, high-performance, critical computing
2. A language that feels natural to write and read with an adaptable learning curve
3. A language that can be extended (see macros and meta-programming)
4. A language that can be learned in less than an hour for a programmer

## Features

- Static typing
- Type inference
- Templates/Generics/Macros/Meta-programming in general
- Memory safety (like a borrow checker)
- Concurrency
- No try/catch, only Result and Option types
- Pattern matching
- Extensible via 'extensions'
- C/C++ interoperability out of the box
- Standard library with the most common needs

## About this

This guide is a work in progress, general ideas and features of Orbis. Think it as a small specification.
Things may change, be removed or added and here is a list of no done things:

- Memory management
- Strings
- Standard library
- Lifetime management
- SoA and AoS
- Macros and meta-programming
- Annotations or attributes

## Syntax

It will be based in the C-Syntax with some Rust, Kotlin and Zig influences.

### Move and copy semantics

The main difference with other langues will be the 'move semantics'.
The '=' operator copies values, while the '<-' operator moves values. For example:

```ts
mut let a = 10; // copy
let b <- 20;    // move (same as let b = 10; but with move semantics)
let c: u32;     // can define a variable without initialize it (it will be 0 in this case)

c = a;          // a is copied to c, a is still valid
a <- b;         // a = 10, b is dropped


io.print(a); // 20
io.print(c); // 10
io.print(b); // compile error! b is dropped
```

By default any variable declared will be immutable, you need to add the 'mut' keyword to make it mutable.
Also, any variable will be copied by default, unless you use the '<-' operator or force a move.

### Scopes and lifetimes

The language will have a 'scope-based' memory management,
when a scope ends, all variables in the scope will be dropped.

```ts
let a = 10;

{
    // a is in scope
    let a = 30;     // variable shadowing, early a is 'hidden'
    let b = 20;
    io.print(a);    // 30
    io.print(b);    // 20
    // b will be dropped here
}

io.print(a); // 10
io.print(b); // compile error! b is out of scope
```

A scope always return a value; the last expression within the scope will determine this value.

```ts
let a = {
    let b = 10;
    let c = 20;

    b + c
};  // a: u32 = 30
```

### Native types

Orbis will have some basic types out-of-the-box, the integer types are:

| Type | Length (in bytes) | C equivalent | Note |
| --- | --- | --- | ---  |
| u8 | 1 | uint8_t | Unsigned 8-bit |
| i8 | 1 | int8_t | Signed 8-bit |
| u16 | 2 | uint16_t | Unsigned 16-bit |
| i16 | 2 | int16_t | Signed 16-bit |
| u32 | 4 | uint32_t | Unsigned 32-bit |
| i32 | 4 | int32_t | Signed 32-bit |
| u64 | 8 | uint64_t | Unsigned 64-bit |
| i64 | 8 | int64_t | Signed 64-bit |
| u128 | 16 | uint128_t | Unsigned 128-bit |
| i128 | 16 | int128_t | Signed 128-bit |
| u256 | 32 | uint256_t | Unsigned 256-bit |
| i256 | 32 | int256_t | Signed 256-bit |

The floating-point are based on IEEE 754:

| Type | Length (in bytes) | C equivalent | Note |
| --- | --- | --- | ---  |
| f16 | 2 | ? | 16-bit floating-point |
| f32 | 4 | float | 32-bit floating-point |
| f64 | 8 | double | 64-bit floating-point |
| f128 | 16 | ? | 128-bit floating-point |
| f256 | 32 | ? | 256-bit floating-point (may be removed) |

Chars in the other hand will be implemented as aliases of:

| Type | Length (in bytes) | C equivalent | Note |
| --- | --- | --- | ---  |
| c8 | 1 | char | See u8 type (ASCII) |
| c16 | 2 | char16_t | See u16 type (UTF-16) |
| c32 | 4 | char32_t | See u32 type (UTF-32) |

Strings will not be a native type, they will be more like a 'composite' type, more on this later.

> [!WARNING]
> Define how the Strings will be implemented

Booleans will be a native type, but they will more like a 'bit-set'. Later will be explained.
Important to know, you can define your own types or aliases to the native types.

```ts
type Int = i32;
type Float = f32;
```

### Initialization values

All variables are initialized with the 'initial value' of their type, for example:

```ts
let a: i32; // 0
let b: f32; // 0.0
let c: b8;  // false or 0
```

### Bit-sets

A bit-set will be a type that can store a arbitrary number of bits, for example:

```ts
let a: b8   // 8 bits or traditional 'bool'
let b: b16  // 16 bits
let c: b3;  // 3 bits
```

This allow a easy way to store flags and other bit-based data, also provides a good way to create padding in structs or classes,
using the least amount of memory possible.

### Operators

| Operator | Description |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |
| & | Bitwise AND |
| \| | Bitwise OR |
| ^ | Bitwise XOR |
| ~ | Bitwise NOT |
| << | Bitwise left shift |
| >> | Bitwise right shift |
| && | Logical AND |
| \|\| | Logical OR |
| ! | Logical NOT |
| == | Equal |
| != | Not equal |
| < | Less than |
| <= | Less than or equal |
| > | Greater than |
| >= | Greater than or equal |
| & | Reference |
| <- | Move |
| ? | Safe call |
| !! | Null panic |

More operators may be added. Also, Like in Zig it will have the 'normal' operators, the
'saturating' operators and the 'wrapping' operators.

```ts
let a = 255;

// let b = a + 1;   // compile error!
let c = a %+ 1      // ok, c = 0
let d = a |+ 1      // ok, d = 255
```

### Control flow

Orbis will have: if, for and do-for loops.

```ts
let a = 10;
if (a == 10) {
    io.print("a is 10");
} else {
    io.print("a is not 10");
}

let b = if (a == 10) 20 else 30;    // ternary operator are replaced by inline if

for (let i = 0; i < 10; i++) {
    io.print(i);
}

let k = 0;
do {
    io.print(k);
} for (k < 10; k++);   // do-for loop, initial value is optional
```

### Functions

Functions will be first-class citizens, you can pass them as arguments, return them and store them in variables.

```ts
fn add(a: i32, b: i32): i32 {   // a and b are copied (see last line)
    return a + b;               // return is a implicit move
}

let a = 10;
let b = 20;

let c = add(a, b);  // copied a and b

io.print(a);        // 10
io.print(b);        // 20
io.print(c);        // 30
```

Also you can move values to functions:

```ts
fn add(a: i32, b: i32): i32 { // a and b are moved (see last line)
    return a + b;               // return is a implicit move
}

let a = 10;
let b = 20;

let c = add(<-a, <-b);  // moved a and b

io.print(a);    // compile error! a is moved
io.print(b);    // compile error! b is moved
io.print(c);    // 30
```

Other feature is that you can force a move value:

```ts
fn add(a: i32, @move b: i32): i32 {
    return a + b;
}

let a = 10;
let b = 20;

add(a, b);      // compile error! b need to be moved
add(a, <-b);    // forced to move b
```

### Structs

Structs will be the main way to create data structures, they will be similar to C or Rust structs.

```ts
struct Point {
    x: f32; // public, can't be changed
    y: f32;
}
```

Struct are only immutable data, you can add the 'mut' keyword to make it mutable:

```ts
struct Point {
    mut x: f32;
    mut y: f32;
}
```

### Classes

Classes are similar to structs, but they can have methods. They will be similar to C++ classes.

> [!WARNING]
> Classes may be removed in the future, because they are a 'syntax sugar' for composites.
> They currently exist to facilitate C++ compatibility.

```ts
class Point {
    x: f32; // private and constant by default
    y: f32;

    pub myValue: f32;   // public
    pro myValue2: f32;  // protected

    pub fn constructor(x: f32, y: f32) {
        this.x = x;
        this.y = y;
    }

    pub fn distance(other: Point): f32 {
        return sqrt((this.x - other.x) * (this.x - other.x) + (this.y - other.y) * (this.y - other.y));
    }
}
```

By default all classes have the 'constructor' and 'destructor' traits.
If you want to modify the value of a class you will need to use the 'mut' keyword:

```ts
class Point {
    mut x: f32;
    mut y: f32;

    pub fn constructor(x: f32, y: f32) {
        this.x = x;
        this.y = y;
    }

    pub fn move(x: f32, y: f32) {
        this.x = x;
        this.y = y;
    }
}
```

Although inheritance is supported, the language encourages composition as the primary design approach.

```ts
class Rectangle {
    x: f32;
    y: f32;
    width: f32;
    height: f32;

    pub fn constructor(x: f32, y: f32, width: f32, height: f32) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }
}

class Square: Rectangle {
    pub fn constructor(x: f32, y: f32, size: f32) {
        super(x, y, size, size);
    }
}
```

### Const and compile-time evaluation

An important point before introducing more advanced features is the 'const' keyword, that will be used to define compile-time values.

```ts
const ALWAYS_IN_SCREAMING_SNAKE_CASE = 10;
let a = ALWAYS_IN_SCREAMING_SNAKE_CASE;     // a = 10
let b <- ALWAYS_IN_SCREAMING_SNAKE_CASE;    // compile error! can't move a const value
const ALWAYS_IN_SCREAMING_SNAKE_CASE = 2;   // compile error! can't re-define a const value
```

The 'const' keyword will be used to define compile-time values, that can be used in the code, for example:

```ts
const PI = 3.1416;

const fn area_of_circle(radius: f32): f32 {
    return PI * radius * radius;
}

let my_circle = area_of_circle(10); // 314.16, calculated at compile-time
```

With the 'const' keyword you cannot:

- const a class or struct
- const a function that have side-effects
- const a function that have a return value that can't be evaluated at compile-time
- const a value that can't be evaluated at compile-time
- const a function that move values

### Atoms

Atoms are a way to define a unique value, they are similar to Erlang atoms, but they act more like a 'tag' than a 'value'.

```ts
let a = :atom1;
let b = :atom2;

if a == b {
    // this will never be executed
}
```

Atoms can't be compared with numbers but internally they will be a unique 64-bit value.

### Enums

Based on atoms, enums are a way to define a set of values.

```ts
enum Color {
    Red,
    Green,
    Blue
}

let a = Color:Red;
```

Enums can have values:

```ts
enum Color {
    Red = 0xFF0000,
    Green = 0x00FF00,
    Blue = 0x0000FF
}
```

Or even can be more complex:

```ts
enum Color {
    RGB(r: b8, g: b8, b: b8),
    CMYK(c: b8, m: b8, y: b8, k: b8)
}

let a = Color:RGB(255, 0, 0);
```

### Pattern matching

Pattern matching is a way to match values with patterns, it is similar to switch-case in C, but more powerful.

```ts
enum Color {
    Red,
    Green,
    Blue
}

fn color_to_string(color: Color): string {
    match color {
        Color:Red -> "Red",
        Color:Green -> "Green",
        Color:Blue -> "Blue"
    }
}
```

Pattern matching can be used with structs and classes:

```ts
struct Point {
    x: f32;
    y: f32;
}

fn point_to_string(point: Point): string {
    match point {
        Point(x, y) -> "Point(" + x + ", " + y + ")"
        Point(x, _) -> "Point(" + x + ", ?)"
        Point(0, 0) -> "Origin"
    }
}
```

### Memory

> [!CAUTION]
> This is under construction, some features may be removed or added

In computers memory has only two possible methods: read and write.
From here, we can derive all the other memory operations, such as:

- Copy (one read, one write)
- Move (one read, two writes)
- Compare (two reads)
- Swap (two reads, two writes)

From this are derived the 'copy' and 'move' semantics along other memory operations in Orbis.

#### References

References are a pointer to a values, think of them as a 'const' pointer in C++.

```ts
let a = 10;
let b = Ref(a); // reference to a

io.print(b); // 10
```

#### Rc and Owner

Rc and Owner are way to handle heap memory, they are similar to C++'s shared_ptr and unique_ptr.
Rc implements a reference counter, as shown in the following example:

```ts
struct Point {
    x: f32;
    y: f32;
}

let point = Rc(Point(10, 20));  // point is now constructed in the heap with a reference count of 1

{
    let point2 = point;             // point2 is now a reference to point, the reference count is now 2
    io.print(point2.x); // 10
    // point2 is dropped, the reference count is now 1
}

io.print(point.x);  // 10
// point is dropped, the reference count is now 0, the memory is freed
```

In the other hand, Owner is a unique owner of the memory:

```ts
struct Point {
    x: f32;
    y: f32;
}

let point = Owner(Point(10, 20));  // point is now constructed in the heap with a reference count of 1

{
    let point2 = point;             // compile error! point is a unique owner
    let point3 <- point;            // point is moved to point3, is now the owner of the memory
    io.print(point3.x); // 10
    // point3 is dropped, the memory is freed
}

io.print(point.x);  // compile error! point is dropped
```

#### Low level memory

Orbis will have a way to manipulate memory in a low level like C, but always the best practice is to use the before mentioned methods.

```ts
let a = 10;
let b = &a; // pointer to a

io.print(b); // address of a
io.print(*b); // 10
```

### Traits

Traits are a way to define a set of methods that a struct or class must implement.
They are similar to interfaces in Java or C# or traits in Rust.

> [!WARNING]
> Expand this section

```ts
trait Drawable {
    pub fn draw();
}

class Shape {
    x: f32;
    y: f32;

    pub fn draw() {
        // draw the shape
    }
}
```

### Composites

Composites are a way to define a 'class' that is composed by other classes.

> [!WARNING]
> Composites may be unified with classes, with the keyword 'use'

```ts
class Drawable {
    color: Color;

    pub fn draw();
}

composite Shape: Drawable {
    // color is inherited from Drawable, but not in the traditional way
    x: f32;
    y: f32;

    pub fn constructor(color: Color, x: f32, y: f32) {
        // super(color); // compile error! composite can't call super because isn't have a 'super'
        this.color = color;
        this.x = x;
        this.y = y;
    }
}
```

For better understanding, the compiler will generate the following code:

```ts
composite Shape {
    color: Color;   // inherited from Drawable
    x: f32;
    y: f32;

    pub fn constructor(color: Color, x: f32, y: f32) {
        this.color = color;
        this.x = x;
        this.y = y;
    }

    pub fn draw();
}
```

### Objects

> [!WARNING]
> Objects may be removed in the future, because they are a 'syntax sugar' for global functions and variables.

Objects are like to 'singleton' in other languages.
Objects can have methods and fields.

```ts
object Math {
    pub fn abs(a: i32): i32 {
        if a < 0 {
            return -a;
        }

        return a;
    }
}

Math.abs(-10);  // 10
```

### SoA and AoS

Structs can have methods if they are 'SoA' (Struct of Arrays) or 'AoS' (Array of Structs).

> [!CAUTION]
> Define how SoA and AoS will be implemented

### Error handling

Inspired by Rust and Kotlin, Orbis will use the 'Result' and 'Option' types to handle errors.

```ts
fn divide(a: i32, b: i32): Result<i32, string> {
    if b == 0 {
        return Err("Division by zero");
    }

    return Ok(a / b);
}

let a = divide(10, 2); // Ok(5)
let b = divide(10, 0); // Err("Division by zero")
```

You can also use atoms to handle errors:

```ts
fn divide(a: i32, b: i32): Result<i32, atom> {
    if b == 0 {
        return Err(:DivisionByZero);
    }

    return Ok(a / b);
}
```

Option is a way to handle optional values:

```ts
fn get_value(a: i32): Option<i32> {
    if a == 0 {
        return None;
    }

    return Some(a);
}
```

### Annotations or Attributes

> [!CAUTION]
> This is under construction, name and syntax may change

Annotations are a way to add metadata to the code, they are similar to C# attributes or Rust's attributes.

```ts
@deprecated("Use the new function")
fn old_function() {
    // old code
}
```

Annotations can be used as a compiler hint, developer documentation, add metadata
to the code (like \_\_attribute__ in GCC) or even manipulate the code.

### Templates or Generics

> [!WARNING]
> This is under construction, name and syntax may change

Templates are a way to define a function or a struct that can be used with different types. They are compile-time evaluated.

```ts
fn add(a: #T, b: #T): #T {
    return a + b;
}

let a = add(10, 20);    // 30
let b = add(9.5, 20.5); // 30.0

let c = add(10.0, 20);      // compile error! can't add a f32 with a i32 (type mismatch)
let d = add#T(10.0, 20.0);  // compile error! can't return a f32 as a u32
```

Also, they can infer the type when it's possible:

```ts
struct Point {
    x: f32;
    y: f32;
}
let a: Rc<Point> = Rc(Point(10, 20)); 
// is the same as
let b = Rc(Point(10, 20));
```

### Modules

Modules are the way to: organize the code, avoid name conflicts, and create a 'namespace'.

```ts
export module math {    // export is needed if you want to use the module outside the file
    pub fn abs(a: i32): i32 {
        if a < 0 {
            return -a;
        }

        return a;
    }
} 
```

Unexported variables, functions, etc. cannot be used outside the file. This is useful to
create 'private' functions or variables without the need to create a class.

### Macros and Meta-programming

> [!CAUTION]
> Research is needed to define how macros will be implemented

## Extensions

Extensions are a way to incorporate (or even eliminate) new features to the language via macros.
By definition only exist three types of extensions: 'superset', 'subset' and 'behavior'.

- Superset: Add new features to the language like new types, operators, keywords, etc.
- Subset: Opposite to 'superset', remove features from the language.
- Behavior: Don't add or remove features, but change the behavior of the language.

### Reactive extension

This extension will add the 'reactive programming' to the language, it will be based on the 'Observer' pattern.
To enable reactive extension you need to: pass the '-extension=reactive' flag to the compiler and start the variables or functions with '$'.
Also you can use the '@reactive' annotation.

```ts
@reactive
fn add(a: i32, b: i32): i32 {
    return a + b;
}

mut let $a = 10;
mut let $b = 20;

let $c = add($a, $b);   // $c = 30
$a = 20;                // $c = 40
```

### GPU extension

The propose of this extension is to enable the compilation of the code to run in a GPU.
To enable GPU extension you need to: pass the '-extension=gpu' flag to the compiler.
This will:

- Remove the standard library
- Remove bit-sets, 128-bit and larger types
- Remove classes, composites, objects and traits
- Remove pattern matching
- Import by default the 'math' module
- Import by default the 'gpu' module

## Tooling

- orb: The compiler will be written over LLVM platform.
- orb-format: The code formatter.
- orb-lsp: The language server protocol.
- orb-prof: The profiler.
- orb-doc: The documentation generator.
- orb-test: The test runner.

## Roadmap

It doesn't exist a roadmap yet, but the first step is to create a MVP (Minimum Viable Product) with the basic features, so:

- PoC (Proof of Concept) of the language: implement the basic features as a clang plugin
- v0.1: Implement the basic features in the compiler
- v0.2: Implement the standard library
- Until v1.0: Iterate over the language, add new features, remove others, etc.
- v0.9: Feature freeze, only bug fixes
- v1.0: Release, the language is stable

After the v1.0 the development will be separated in two types of releases: 'major' and 'minor'.

- Major releases can introduce breaking changes
- Minor changes only can be bugfixes or patches

With this approach the language don't need to have an 'LTS' version, major versions will be.
In the far future the develop of an v2.0 may start, but it will feel like a new language, not a new version.

## Additional notes

- Due compatibility, Orbis will need at least AVX compatible CPUs
- All things are subject to change
- The official serialization formats will be: YAML for human readability, binary for performance
- The build system will be the language itself
- All configs will be in YAML format

## License

Everything related to Orbis will be under the MIT license, everyone can use it without restrictions.

## Why?

Section to explain some questions. This section and the next are opinionated.

### Why create a new language?

Because me, the author, have a specific need: a language that can be implemented in my own game engine. Also, I want to create something new
and learn from the process. I have been coding in the last +10 years (I'm 23 at the time of writing this), and I want to create something that I can be proud of.
Also, I saw a lot of languages that are good, but they are not perfect, so I want to create something that can be perfect for me and, maybe, for others.

### Why the name 'Orbis'?

Initially it was only a codename but I like it.

### Why no 'static' keyword?

The 'static' keyword have little to no sense in a no forced OOP language. It usually hides an architectural problem instead of resolving it.
Also, 'static' in many languages is actually 'syntatyc sugar' for other things.

### Why meta-programming?

Meta-programming is a extremely powerful tool that enables the developer to write less code, making the iteration faster and the code more readable.
Also, Orbis is a extremely modular language, so meta-programming is a must. The standard library will use a lot of meta-programming.

## Philology

- Is better to crash than to bug
- The best code is the no code
- Programming languages must adapt to developers, not the other way around
- Compile time is near infinite
- Resources of the end user are limited
- 80% of the work takes 20% of the time
