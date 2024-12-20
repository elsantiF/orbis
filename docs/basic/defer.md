# Defer

`defer` is a statement that allows you to execute a block or line of code when the current scope is exited.
This is useful for cleaning up resources, such as closing files or freeing memory.

```rs
let file = io.open("file.txt", io.Mode.Read);
defer io.close(file);

// do something with the file
```

The `defer` statement will execute the code in the reverse order that it was declared.

```rs
defer {
    io.print("world");
    io.print("hello");
}

// Output: hello world
```

You can `defer` based on a condition:

```rs
let a = 5;
defer if a > 0 {
    io.print("a is greater than 0");
}
```
