# Reactive Extension

This extension will add the 'reactive programming' to the language, it will be based on the 'Observer' pattern.
To enable reactive extension you need to: pass the '-extension=reactive' flag to the compiler and start the variables or functions with '$'.
Also you can use the '@reactive' attribute.

```ts
@reactive
fn add(a: i32, b: i32): i32 {
    return a + b;
}

mut let $a = 10;
mut let $b = 20;

let $c = add($a, $b);   // $c = 30
$a = 20;                // $c = 40
```
