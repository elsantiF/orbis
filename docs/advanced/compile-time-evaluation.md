# Const and compile-time evaluation

An important point before introducing more advanced features is the `const` keyword, that will be used to define compile-time values.

```ts
const ALWAYS_IN_SCREAMING_SNAKE_CASE = 10;
let a = ALWAYS_IN_SCREAMING_SNAKE_CASE;     // a = 10
let b <- ALWAYS_IN_SCREAMING_SNAKE_CASE;    // compile error! can't move a const value
const ALWAYS_IN_SCREAMING_SNAKE_CASE = 2;   // compile error! can't re-define a const value
```

The `const` keyword will be used to define compile-time values, that can be used in the code, for example:

```ts
const PI = 3.1416;

const fn area_of_circle(radius: f32): f32 {
    return PI * radius * radius;
}

let my_circle = area_of_circle(10); // 314.16, calculated at compile-time
```

With the `const` keyword you can't:

- const a class or struct
- const a function that have side-effects
- const a function that have a return value that can't be evaluated at compile-time
- const a value that can't be evaluated at compile-time
- const a function that move values
