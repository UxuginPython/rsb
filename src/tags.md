# Tags

## Special Tags

|Name      |`i8`|Function                                    |
|----------|----|--------------------------------------------|
|`SKIP_1`  |-128|Do not search for a tag in the next byte.   |
|`SKIP_2`  |-127|Do not search for tags in the next 2 bytes. |
|`SKIP_4`  |-126|Do not search for tags in the next 4 bytes. |
|`SKIP_8`  |-125|Do not search for tags in the next 8 bytes. |
|`SKIP_16` |-124|Do not search for tags in the next 16 bytes.|
|`SKIP_U8` |-123|Read the `u8` value of the next byte. Add 1 and do not search for tags in that number of bytes after it.|
|`SKIP_U16`|-122|Read the `u16` value of the next 2 bytes. Add 1 and do not search for tags in that number of bytes after them.|

## Matched Tags

|Name         |`i8`|Function                    |
|-------------|----|----------------------------|
|`NODES_START`|1   |Begin a node list.          |
|`NODES_END`  |-1  |End a node list.            |
|`NODE_START` |2   |Begin a node in a node list.|
|`NODE_END`   |-2  |End a node in a node list.  |
