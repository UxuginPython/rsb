# Tag Tree

RSB uses an XML-like tag system called the "tag tree" for internal organization. This system is designed for both extensibility and backwards compatibility. Unlike XML though, RSB is a binary format. Each tag has a constant `i8` value.

Tags come in two types: matched and unmatched. Matched tags affect everything between an opening and a closing tag. They are generally used for things of varying length or things whose length is likely to change in future versions of the specification. Unmatched tags affect a certain fixed number of bytes after a single tag. They can save a bit of space in some places but are much less extensible, so they are used relatively sparingly.

## Skip Tags: Fixed and Variable

### Fixed Skip Tags

`SKIP_N` instructs the interpreter to not search for tags within the following N bytes.

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
`N` here means that a byte is skipped during tag searching and `Y` means that it is checked for tags. `SKIP_U8` can skip up to 256 bytes.

`SKIP_U16` (-122): Read the `u16` value of the next 2 bytes. Add 1 and do not search for tags for that number of bytes after them. For example, one may see the following in a file:
```ignore
SKIP_U16 4u16 N N N N N Y
```
`N` and `Y` mean the same as above. Note that `4u16` takes up two bytes. `SKIP_U16` can skip up to 64KiB.
