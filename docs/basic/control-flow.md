# Control flow

Orbis will have: if, for and do-for loops.

```ts
let a = 10;
if (a == 10) {
    io.print("a is 10");
} else {
    io.print("a is not 10");
}

let b = if (a == 10) 20 else 30;    // ternary operator are replaced by inline if

for (let i = 0; i < 10; i++) {
    io.print(i);
}

let k = 0;
do {
    io.print(k);
} for (k < 10; k++);   // do-for loop, initial value is optional
```
