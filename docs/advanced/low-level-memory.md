# Low level memory

> ![WARNING]
> This is a work in progress, expand this section with more information.

Orbis will have a way to manipulate memory in a low level like C, but always the best practice is to use the before mentioned methods.

```ts
let a = 10;
let b = &a; // pointer to a

io.print(b); // address of a
io.print(*b); // 10
```
