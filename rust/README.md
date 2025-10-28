# rust

## binary vs library

whether you are building a binary or a library

- binary: building a program that someone is going to run from the CLI
- library: everything else

sometimes building something that has both a binary and a library

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

## use of `match` versus `if let Some(x)`

- use match if you care about more than one of the patterns
- otherwise use the `if let Some(x)`

## anonymous lifetimes

- use the anonymous lifetime if you can, e.g. `<'_>`

## `<>` are used for generics 

