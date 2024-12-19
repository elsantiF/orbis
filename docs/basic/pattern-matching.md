# Pattern matching

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
