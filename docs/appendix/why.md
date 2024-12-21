# Why?

Section to explain some questions. This section and the next are opinionated.

## Why create a new language?

Because me, the author, have a specific need: a language that can be implemented in my own game engine. Also, I want to create something new
and learn from the process. I have been coding in the last +10 years (I'm 23 at the time of writing this), and I want to create something that I can be proud of.
Also, I saw a lot of languages that are good, but they are not perfect, so I want to create something that can be perfect for me and, maybe, for others.

## Why the name 'Orbis'?

Initially it was only a codename but I like it.

## Why no 'static' keyword?

The 'static' keyword have little to no sense in a no forced OOP language. It usually hides an architectural problem instead of resolving it.
Also, 'static' in many languages is actually 'syntactic sugar' for other things.

## Why meta-programming?

Meta-programming is a extremely powerful tool that enables the developer to write less code, making the iteration faster and the code more readable.
Also, Orbis is a extremely modular language, so meta-programming is a must. The standard library will use a lot of meta-programming.

## Why no 'try/catch'?

I think that the 'try/catch' system can be used in some cases to not handle errors, but instead hide them, like in global error handlers. Also,
from a performance perspective, they provide a lot of overhead. The replacement with 'Result' and 'Option' types is more explicit and more efficient.

## Why no 'null' (only for optionals)?

`null` is a special value in many languages but it have no sense from a memory perspective because it's value is not other than a pointer to the memory address 0.
This causes that developers can use `null` in many cases where they should not. I think that a better approach is to use `Option` and `Result` types, they force the developer to handle the cases where the value is `null` or the operation fails.
