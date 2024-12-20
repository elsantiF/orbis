# High Level Memory

> [!CAUTION]
> This is under construction, some features may be removed or added

In computers memory has only two possible methods: read and write.
From here, we can derive all the other memory operations, such as:

- Copy (one read, one write)
- Move (one read, two writes)
- Compare (two reads)
- Swap (two reads, two writes)

From this are derived the 'copy' and 'move' semantics along other memory operations in Orbis.

## References

References are a pointer to a values, think of them as a 'const' pointer in C++.

```ts
let a = 10;
let b = Ref(a); // reference to a

io.print(b); // 10
```

## Rc and Owner

Rc and Owner are way to handle heap memory, they are similar to C++'s shared_ptr and unique_ptr.
Rc implements a reference counter, as shown in the following example:

```ts
struct Point {
    x: f32;
    y: f32;
}

let point = Rc(Point(10, 20));  // point is now constructed in the heap with a reference count of 1

{
    let point2 = point;             // point2 is now a reference to point, the reference count is now 2
    io.print(point2.x); // 10
    // point2 is dropped, the reference count is now 1
}

io.print(point.x);  // 10
// point is dropped, the reference count is now 0, the memory is freed
```

In the other hand, Owner is a unique owner of the memory:

```ts
struct Point {
    x: f32;
    y: f32;
}

let point = Owner(Point(10, 20));  // point is now constructed in the heap with a reference count of 1

{
    let point2 = point;             // compile error! point is a unique owner
    let point3 <- point;            // point is moved to point3, is now the owner of the memory
    io.print(point3.x); // 10
    // point3 is dropped, the memory is freed
}

io.print(point.x);  // compile error! point is dropped
```
