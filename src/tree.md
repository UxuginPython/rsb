# Tag Tree

RSB uses an XML-like tag system called the "tag tree" for internal organization. This system is designed for both extensibility and backwards compatibility. Unlike XML though, RSB is a binary format. Each tag has a constant `i8` value.

Tags come in two types: matched and unmatched. Matched tags affect everything between an opening and a closing tag. They are generally used for things of varying length or things whose length is likely to change in future versions of the specification. Unmatched tags affect a certain fixed number of bytes after a single tag. They can save a bit of space in some places but are much less extensible, so they are used relatively sparingly.

With matched tags, there must be a 1:1 matchup between start and end tags. Additionally, before an outer block can be closed, all of its nested inner blocks must be fully closed, e.g., the following is not allowed:

```ignore
X_START Y_START X_END Y_END
                |     |
                |     doesn't make sense outside of X block
                |
                X closed before inner Y
```

## Skip Tags: Fixed and Variable

Skip tags are used to skip a certain number of bytes when searching for tags. This is useful when storing raw numerical information that may unintentionally contain tag bytes which should not be read.

### Fixed Skip Tags

`SKIP_N` instructs the interpreter to not search for tags within the following N bytes.

```ignore
SKIP_2 N N Y
```

`N` here means that a byte is skipped during tag searching and `Y` means that it *is* checked for tags. `SKIP_2`, of course, skips 2 bytes.

|Name      |Value|
|----------|-----|
|`SKIP_1`  |-128 |
|`SKIP_2`  |-127 |
|`SKIP_4`  |-126 |
|`SKIP_8`  |-125 |
|`SKIP_16` |-124 |

### Variable Skip Tags

`SKIP_U8` (-123): Read the `u8` value of the next byte. Add 1 and do not search for tags for that number of bytes after it. For example, one may see the following in a file:
```ignore
SKIP_U8 3u8 N N N N Y
```

`N` and `Y` mean the same as above. `SKIP_U8` can skip up to 256 bytes.

`SKIP_U16` (-122): Read the `u16` value of the next 2 bytes. Add 1 and do not search for tags for that number of bytes after them. For example, one may see the following in a file:
```ignore
SKIP_U16 4u16 N N N N N Y
```

Note here that `4u16` takes up two bytes. `SKIP_U16` can skip up to 64KiB.
