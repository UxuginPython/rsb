# Example

Here is an example of a file containing two nodes, each with two inputs, with the first input of the second node connected to the output of the first node. All other inputs are disconnected.

```ignore
rrtkstrmbldr 1u8 0u8 0u8 0u8
NODE_SECTION_START
    NODE_START
        NODE_ID SKIP_2 0u16
        COORDINATES SKIP_16 0.0f64 0.0f64
        NODE_INPUT_LIST_START SKIP_U8 3u8 //Remember that SKIP_U8 skips this number + 1.
            65535u16
            65535u16
        NODE_INPUT_LIST_END
    NODE_END
    NODE_START
        NODE_ID SKIP_2 0u16
        COORDINATES SKIP_16 300.0f64 0.0f64
        NODE_INPUT_LIST_START SKIP_U8 3u8
            0u16
            65535u16
        NODE_INPUT_LIST_END
    NODE_END
NODE_SECTION_END
```
