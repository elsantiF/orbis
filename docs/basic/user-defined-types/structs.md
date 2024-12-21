# Structs

Structs will be the main way to create types, they will be similar to C or Rust structs.

```ts
struct Point {
    x: f32; // public, can't be changed
    y: f32;
}
```

Struct are only immutable data, you can add the `mut` keyword to make it mutable:

```ts
struct Point {
    mut x: f32;
    mut y: f32;
}
```

Like in Go, you can create a method for a struct:

```ts
struct Point {
    x: f32;
    y: f32;
}

fn (p: Point) distance(other: Point): f32 {
    return Math.sqrt((p.x - other.x) * (p.x - other.x) + (p.y - other.y) * (p.y - other.y));
}
```

To enable some kind of inheritance, and to not use composition, you can use the `use` keyword:

```ts
struct Point {
    x: f32;
    y: f32;
}

struct Point3D {
    use Point; // x and y will be in Point3D
    z: f32;
}

let p = Point3D { x: 1.0, y: 2.0, z: 3.0 };
```

For better understanding, the `use` keyword is similar to the `extends` keyword in other languages.
The compiler will copy the fields and methods from the `Point` struct to the `Point3D` struct.
