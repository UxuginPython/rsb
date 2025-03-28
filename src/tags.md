# Tag Index

Every tag has an associated `i8` value. See the [Tag Tree](./tree.md) chapter for information about matched and unmatched tags.

Tags notated with a * are reserved but not currently supported.

## Unmatched

|Name                 |Value|
|---------------------|-----|
|`SKIP_1`             |-128 |
|`SKIP_2`             |-127 |
|`SKIP_4`             |-126 |
|`SKIP_8`             |-125 |
|`SKIP_16`            |-124 |
|`SKIP_U8`            |-123 |
|`SKIP_U16`           |-122 |
|`NODE_ID`            |0    |
|`NODE_COORDINATES`   |3    |
|`RRTK_TARGET_VERSION`|6    |
|`WINDOW_COORDINATES`*|7    |
|`WINDOW_ZOOM`*       |8    |

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
|`NODE_VAR_NAME_START`* |5    |
|`NODE_VAR_NAME_END`*   |-5   |
|`LIBRARY_NAME_START`   |9    |
|`LIBRARY_NAME_END`     |-9   |
|`LIBRARY_VERSION_START`|10   |
|`LIBRARY_VERSION_END`  |-10  |
|`EXTENSION_INFO_START` |11   |
|`EXTENSION_INFO_END`   |-11  |
|`COMMENT_START`        |12   |
|`COMMENT_END`          |-12  |
