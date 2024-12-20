# Native types

Orbis will have some basic types out-of-the-box, the integer types are:

| Type | Length (in bytes) | C equivalent | Note |
| --- | --- | --- | ---  |
| u8 | 1 | uint8_t | Unsigned 8-bit |
| i8 | 1 | int8_t | Signed 8-bit |
| u16 | 2 | uint16_t | Unsigned 16-bit |
| i16 | 2 | int16_t | Signed 16-bit |
| u32 | 4 | uint32_t | Unsigned 32-bit |
| i32 | 4 | int32_t | Signed 32-bit |
| u64 | 8 | uint64_t | Unsigned 64-bit |
| i64 | 8 | int64_t | Signed 64-bit |
| u128 | 16 | uint128_t | Unsigned 128-bit |
| i128 | 16 | int128_t | Signed 128-bit |
| u256 | 32 | uint256_t | Unsigned 256-bit |
| i256 | 32 | int256_t | Signed 256-bit |

The floating-point are based on IEEE 754:

| Type | Length (in bytes) | C equivalent | Note |
| --- | --- | --- | ---  |
| f16 | 2 | ? | 16-bit floating-point |
| f32 | 4 | float | 32-bit floating-point |
| f64 | 8 | double | 64-bit floating-point |
| f128 | 16 | ? | 128-bit floating-point |
| f256 | 32 | ? | 256-bit floating-point (may be removed) |

Chars in the other hand will be implemented as aliases of:

| Type | Length (in bytes) | C equivalent | Note |
| --- | --- | --- | ---  |
| c8 | 1 | char | See u8 type (ASCII) |
| c16 | 2 | char16_t | See u16 type (UTF-16) |
| c32 | 4 | char32_t | See u32 type (UTF-32) |

Strings will not be a native type, they will be more like a 'composite' type, more on this later.

> [!WARNING]
> Define how the Strings will be implemented

Booleans will be a native type, but they will more like a 'bit-set'. Later will be explained.
Important to know, you can define your own types or aliases to the native types.

```ts
type Int = i32;
type Float = f32;
```

## Initialization values

All variables are initialized with the 'initial value' of their type, for example:

```ts
let a: i32; // 0
let b: f32; // 0.0
let c: b8;  // false or 0
```

## Bit-sets

A bit-set will be a type that can store a arbitrary number of bits, for example:

```ts
let a: b8;  // 8 bits or traditional 'bool'
let b: b16; // 16 bits
let c: b3;  // 3 bits
```

This allow a easy way to store flags and other bit-based data, also provides a good way to create padding in structs or classes,
using the least amount of memory possible.

## Operators

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

More operators may be added. Also, Like in Zig it will have the 'normal' operators, the
'saturating' operators and the 'wrapping' operators.

```ts
let a = 255;

let b = a + 1;  // compile error!
let c = a %+ 1; // ok, c = 0
let d = a |+ 1; // ok, d = 255
```
