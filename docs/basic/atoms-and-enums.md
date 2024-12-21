# Atoms and Enums

## Atoms

> [!WARNING]
> Atoms may be renamed to Symbols in the future.

Atoms are a way to define a unique value, they are similar to Erlang atoms, but they act more like a 'tag' than a 'value'.

```ts
let a = :atom1;
let b = :atom2;

if a == b {
    // this will never be executed
}
```

Atoms can't be compared with numbers but internally they will be a unique 64-bit value.

## Enums

Based on atoms, enums are a way to define a set of atoms.

```ts
enum Color {
    Red,
    Green,
    Blue
}

let a = Color:Red;
```

Enums can have values:

```ts
enum Color {
    Red = 0xFF0000,
    Green = 0x00FF00,
    Blue = 0x0000FF
}
```

Or even can be more complex:

```ts
enum Color {
    RGB(r: b8, g: b8, b: b8),
    CMYK(c: b8, m: b8, y: b8, k: b8)
}

let a = Color:RGB(255, 0, 0);
```
