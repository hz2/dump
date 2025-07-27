# rust

- mutability controls whether you can change a value

## lifetimes

- use `<'a>` inside angle brackets when you are declaring a generic lifetime 
- lifetimes control how long a reference lives
    - borrowing a book from a lib for some time
- `<>` used for generics, e.g. `<T>`
    - `<'a>` introduces a _named_ lifetime
  parameter for a function, `struct`, `enum`, or `impl` block

```rust
fn foo<'a>(x: &'a str) -> &'a str {
    x
}
```
- `'a` is the lifetime parameter
- `x: &'a str` means: "the reference `x` must live at least as long as `'a`"
- `-> &'a str` means: "the return value lives as long as `'a` too"
- the returned reference must not outlive the input reference
