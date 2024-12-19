# Generics

> [!WARNING]
> This is under construction, name and syntax may change

Templates are a way to define a function or a struct that can be used with different types. They are compile-time evaluated.

```ts
fn add<T>(a: T, b: T): T {
    return a + b;
}

let a = add(10, 20);    // 30
let b = add(9.5, 20.5); // 30.0

let c = add(10.0, 20);          // compile error! can't add a f32 with a i32 (type mismatch)
let d = add<f32>(10.0, 20.0);   // compile error! can't return a f32 as a u32
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
