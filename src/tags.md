# Tag Index

Every tag has an associated `i8` value. See the [Tag Tree](./tree.md) chapter for information about matched and unmatched tags.

## Unmatched

|Name         |Value|
|-------------|-----|
|`SKIP_1`     |-128 |
|`SKIP_2`     |-127 |
|`SKIP_4`     |-126 |
|`SKIP_8`     |-125 |
|`SKIP_16`    |-124 |
|`SKIP_U8`    |-123 |
|`SKIP_U16`   |-122 |
|`NODE_ID`    |0    |
|`COORDINATES`|3    |

## Matched

Typically, the opening tag of a pair of matched tags is positive and the closing tag is negative, and they have the same absolute value.

|Name                   |Value|
|-----------------------|-----|
|`NODE_SECTION_START`   |1    |
|`NODE_SECTION_END`     |-1   |
|`NODE_START`           |2    |
|`NODE_END`             |-2   |
|`NODE_INPUT_LIST_START`|4    |
|`NODE_INPUT_LIST_END`  |-4   |
