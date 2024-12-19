# Functions

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
