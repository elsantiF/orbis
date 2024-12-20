# Operators

Orbis will provide a set of operators in the language itself, you can define your own operators or overload the existing ones.

| Operator | Description |
| --- | --- |
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |
| & | Bitwise AND |
| \| | Bitwise OR |
| ^ | Bitwise XOR |
| ~ | Bitwise NOT |
| << | Bitwise left shift |
| >> | Bitwise right shift |
| && | Logical AND |
| \|\| | Logical OR |
| ! | Logical NOT |
| == | Equal |
| != | Not equal |
| < | Less than |
| <= | Less than or equal |
| > | Greater than |
| >= | Greater than or equal |
| & | Reference |
| <- | Move |
| ? | Optional / Null check |
| !! | Null panic |
| \|> | Pipe operator |

More operators may be added. \

## Saturating and Wrapping Operators

Also, Like in Zig it will have 'saturating' operators and 'wrapping' operators.

```ts
let a = 255;

let b = a + 1;  // compile error!
let c = a %+ 1; // ok, c = 0
let d = a |+ 1; // ok, d = 255
```

Think it as:

- `%+` executes a `+` and then a `%` operation
- `|+` executes a `if` and, if isn't at the maximum value, executes a `+` operation

## Pipe Operator

The `|>` operator is used to pipe the result of an expression to a function.

```ts
fn double(a: u32) -> u32 {
    return a * 2;
}

fn square(a: u32) -> u32 {
    return a * a;
}

let a = 10;

let b = a |> double |> square; // square(double(a))
```

It's intended to be used as a way to chain functions, like in Elixir.
