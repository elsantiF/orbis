# Modules

Modules are the way to: organize the code, avoid name conflicts, and create a 'namespace'.

```ts
export module math {    // export is needed if you want to use the module outside the file
    pub fn abs(a: i32): i32 {
        if a < 0 {
            return -a;
        }

        return a;
    }
} 
```

Unexported variables, functions, etc. cannot be used outside the file. This is useful to
create 'private' functions or variables without the need to create a class.
