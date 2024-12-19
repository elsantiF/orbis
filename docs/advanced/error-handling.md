 Error handling

Inspired by Rust and Kotlin, Orbis will use the 'Result' and 'Option' types to handle errors.

```ts
fn divide(a: i32, b: i32): Result<i32, string> {
    if b == 0 {
        return Err("Division by zero");
    }

    return Ok(a / b);
}

let a = divide(10, 2); // Ok(5)
let b = divide(10, 0); // Err("Division by zero")
```

You can also use atoms to handle errors:

```ts
fn divide(a: i32, b: i32): Result<i32, atom> {
    if b == 0 {
        return Err(:DivisionByZero);
    }

    return Ok(a / b);
}
```

Option is a way to handle optional values:

```ts
fn get_value(a: i32): Option<i32> {
    if a == 0 {
        return None;
    }

    return Some(a);
}
```
