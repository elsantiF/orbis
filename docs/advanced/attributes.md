# Attributes

> [!CAUTION]
> This is under construction, name and syntax may change

Attributes are a way to add metadata to the code, they are similar to C# attributes or Rust's attributes.

```ts
@deprecated("Use the new function")
fn old_function() {
    // old code
}
```

Attributes can be used as a compiler hint, developer documentation, add metadata
to the code (like \_\_attribute__ in GCC) or even manipulate the code.
