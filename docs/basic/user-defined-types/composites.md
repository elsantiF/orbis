# Composites

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
