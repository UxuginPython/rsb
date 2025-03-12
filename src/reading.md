# Reading the Specification

This specification assumes knowledge of Rust's basic number types (`i32`, `f64`, etc.) as well as a bit of familiarity with [semantic versioning](https://semver.org/spec/v2.0.0.html). Experience with tag-based formats (XML, HTML, etc.) will also be useful but is not necessary. This specification is fairly simple and there is not a lot of background knowledge required. However, there are a couple things that may not be immediately obvious.

## "`TAG` (value)" Syntax

As you will read [later](tree.md), the RSB format uses an XML-like tag system except binary. Every tag has an `i8` value. Often, tags will be written as `TAG` (#) where the number in parentheses is this `i8` value, e.g., `COORDINATES` (3).

## Examples

The specification will occasionally provide examples of the layout of a concept. However, providing actual bytes or hex codes would prove quite inconvenient, so they are written like this:

```ignore
SKIP_U8 15u8 x_f64 y_f64
```

This example is composed of a tag (an `i8`), a `u8`, and two `f64`s concatenated. **Elements of an example may vary in byte count,** as is seen here. Whitespace may vary for readability, but all elements must be immediately concatenated.
