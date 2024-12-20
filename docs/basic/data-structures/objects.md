# Objects

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
