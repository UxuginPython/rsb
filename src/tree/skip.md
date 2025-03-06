# Skip Tags: Fixed and Variable

## Fixed Skip Tags

`SKIP_N` instructs the interpreter to not search for tags within the following N bytes.

|Name      |Value|
|----------|-----|
|`SKIP_1`  |-128 |
|`SKIP_2`  |-127 |
|`SKIP_4`  |-126 |
|`SKIP_8`  |-125 |
|`SKIP_16` |-124 |

## Variable Skip Tags

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
