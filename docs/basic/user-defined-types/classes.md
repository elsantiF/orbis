# Classes

Classes are similar to structs, but they can have methods defined inside them.
They will be similar to C++ classes.

> [!WARNING]
> Classes may be removed in the future, because they are a 'syntax sugar' for composites.
> They currently exist to facilitate C++ compatibility.
> Also, inheritance may be changed in favor of composition and `use`.

```ts
class Point {
    x: f32; // private and constant by default
    y: f32;

    pub myValue: f32;   // public
    sub myValue2: f32;  // sub is like protected in other languages

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

Important to note: classes are defined as 'macros' in the 'core' layer, and are not part of the language itself.
