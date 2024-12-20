# Low level memory

> ![WARNING]
> This is a work in progress, expand this section with more information.

Orbis will have a way to manipulate memory in a low level like C, but always the best practice is to use the before mentioned methods.

## Pointers

Pointers are a way to access memory directly, they are a reference to a memory address.

```ts
let a = 10;
let b = &a; // b is a pointer to a

io.print(*b); // 10
io.print(b);  // some memory address
```

The `&` operator is used to get the memory address of a variable, and the `*` operator is used to get the value of the memory address.
The type of a pointer is `*T`, where `T` is the type of the variable.

## Pointer arithmetic

Pointer arithmetic is a way to move the pointer to another memory address. To allow this you need to use the `unsafe` keyword.

```ts
let a = 10;
mut let b = &a; // b is a pointer to a

unsafe {
    b += 1; // move the pointer to the next memory address
}

io.print(*b); // some random value
```
