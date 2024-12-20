# Syntax

It will be based in the C-Syntax with some Rust, Kotlin and Zig influences.

## Move and copy semantics

The main difference with other langues will be the 'move semantics'.
The `=` operator copies values, while the `<-` operator moves values. For example:

```ts
mut let a = 10; // copy
let b <- 20;    // move (same as let b = 10; but with move semantics)
mut let c: u32; // can define a variable without initialize it (it will be 0 in this case)

c = a;          // a is copied to c, a is still valid
a <- b;         // a = 10, b is dropped


io.print(a); // 20
io.print(c); // 10
io.print(b); // compile error! b is dropped
```

By default any variable declared will be immutable, you need to add the `mut` keyword to make it mutable.
Also, any variable will be copied by default, unless you use the `<-` operator or force a move.

## Scopes and lifetimes

The language will have a 'scope-based' memory management,
when a scope ends, all variables in the scope will be dropped.

```ts
let a = 10;

{
    // a is in scope
    let a = 30;     // compile error! a is already defined
    let b = 20;
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
