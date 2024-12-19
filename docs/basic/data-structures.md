# Data Structures

## Structs

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

## Classes

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

## Composites

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

## Objects

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
