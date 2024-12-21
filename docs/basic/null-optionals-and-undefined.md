# Null, Optionals and Undefined

## Null and Optionals

> [!WARNING]
> `null` may be removed, also 'Optionals' can become part of the 'core' layer instead of the language itself.

`null` is a special value in many languages that represents the absence of a value. This can lead to many issues, such as null pointer exceptions (Java and C#). In Orbis, `null` is not a special value, but rather a type. This means that you can't assign `null` to a variable unless it is explicitly typed as `null`.

```rs
mut let a: u32?; // a is an optional u32, by default it is null
io.print(a); // compiler error! a is null

a = 10;

if (a) {
    io.print(a); // ok, a = 10
}

io.print(a); // also ok, a = 10

a = null; // ok, you can assign null to a
```

To reduce the code verbosity, you can use the `?` operator to check if an optional is `null` or not.

```rs
mut let a: s8? = "Hello";

if (a?.length() > 0) { // only executes if a is not null and has a length greater than 0
    io.print("a is not null and has a length greater than 0");
} else {
    io.print("a is null or has a length of 0");
}
```

## Undefined

By default, all variables have an 'initial value', even if you don't assign one. `undefined` is a
special value that works like C and C++'s utilized variables. You can't use the variable until you assign a value to it.

```rs
mut let a: u32 = undefined; // a is undefined, it's a garbage value
io.print(a); // compiler error! a is undefined
a = 10;
io.print(a); // ok, a = 10
```

Remember that `undefined` is not the same as `null`. `undefined` is a garbage value, while `null` is a special value that represents the absence of a value.
Also, don't abuse `undefined` in your code, it's present only for compatibility with C and C++.

## Null Panics

If you want to panic when an optional is `null` you can use the `!!` operator.

```rs
mut let a: u32? = null;

io.print(a!!); // valid, panics because a is null
```

Use this operator with caution, as it can lead to runtime errors if not used properly.
