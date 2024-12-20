# Memory

Orbis will separate memory into two categories: high-level and low-level memory.

> ![WARNING]
> Some concepts are not yet defined, this is a work in progress.

- **High Level Memory**: Collection of functions and types that abstract the memory operations, they are part of the 'core' layer.
                        This is the default way to handle memory in Orbis.
- **Low Level Memory**: Direct access to memory, this is the way to handle memory in a more 'C' way. Use this only when you need to.

Is important to note that all declared variables are allocated in the stack, to use the heap you need to explicitly allocate it.
