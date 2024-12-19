# Traits

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
        // now the Shape class can be used as a Drawable
    }
}
```
