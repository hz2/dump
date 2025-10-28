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

if you have some value, the lifetime of that value is until the value is 
moved. if the value is never moved then it has a static lifetime.

if you store something on a stack of a given function, the lifetime of that 
value (unless you move it somewhere else) is going to be the lifetime of that 
function and when that function returns, that lifetime ends.
you couldn't give out a reference to something on the stack. that ref can't 
be allowed to continue living after the function returns.

the heap allocation lifetime is alive until it is dropped.
way you can get something on the heap but never drop it is through `BoxLeak`
which has a static reference.

## use of `match` versus `if let Some(x)`

- use match if you care about more than one of the patterns
- otherwise use the `if let Some(x)`

## anonymous lifetimes

- use the anonymous lifetime if you can, e.g. `<'_>`

## `<>` are used for generics and lifetimes

## prefer `assert_eq` over `assert` for nicer errors

## difference between `ref mut T` and `&mut T`

- about where the borrow happens

in the context of `if let` pattern matching

```rust
if let Some(x) = some_option {
    ...
}
```

we are destructuring the value on the right-hand side.

the pattern determines what bindings (and references) you create.

so the pattern between `ref mut` and `&mut` inside a pattern is whether you
are matching a reference or creating one

1. `if let Some(ref mut T) = maybe`
  - `maybe` is an __owned__ `Option<T>`, not an `Option<&mut T>`
  - "if `maybe` is `Some`, borrow the inner value mutably"
  - `T` becomes `&mut T`
  - `ref mut` creates a mutable reference to the inner value.
2. `if let Some(&mut T) = maybe`
  - `maybe` must be an `Option<&mut T>`, i.e. it already contains a mutable
  reference
  - you are destructing that reference: `&mut T` pattern dereferences the 
  inner mutable reference
  - `&mut` matches against an existing mutable reference pattern

imagine you have a box (`Option<T>`) that owns something:

- `ref mut` says don't open the box fully, just give me a mutable peek (`&mut`)
inside
- if you already have a box that contains a reference (`Option<&mut T>`)
  - `&mut` says let me open it and pull out what's being referenced
