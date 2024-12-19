# GPU Extension

The propose of this extension is to enable the compilation of the code to run in a GPU.
To enable GPU extension you need to: pass the '-extension=gpu' flag to the compiler.
This will:

- Remove the standard library
- Remove bit-sets, 128-bit and larger types
- Remove classes, composites, objects and traits
- Remove pattern matching
- Import by default the 'math' module
- Import by default the 'gpu' module
