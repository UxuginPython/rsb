# Node Section

The node section is the most important part of the tag tree. There is exactly one node section in an RSB file. It is composed of a block created by `NODE_SECTION_START` (1) and `NODE_SECTION_END` (-1) tags containing an ordered list of node blocks. **All information in a node section besides nodes must be ignored.**

## Node Blocks

A node block, created with `NODE_START` (2) and `NODE_END` (-2) tags, represents a Stream Builder node. It contains exactly one of each of three things: the type of node, its coordinates, and a list of its inputs. The way these work is fairly intuitive. **All information besides the node ID, coordinates, and its input list must be ignored.**

### `NODE_ID` (0) Tag

```ignore
NODE_ID SKIP_2 id_u16
```

Every node block contains a node ID, which tells what kind of node it is. This is represented by a `NODE_ID` tag, a `SKIP_2` tag, and a `u16` node ID. `NODE_ID` is an unmatched tag. A list of node IDs is provided below:

|Node|ID|
|----|--|

### `COORDINATES` (3) Tag

```ignore
COORDINATES SKIP_16 x_f64 y_f64
```

Another element of every node block is its coordinates. The `COORDINATES` tag simply holds two `f64`s (for x and y) after a `SKIP_16`. It too is an unmatched tag. The following is also allowed:

```ignore
COORDINATES SKIP_8 x_f64 SKIP_8 y_f64
```

### Input List

```ignore
NODE_INPUT_LIST_START SKIP_U8 (input count * 2)u8
    input_u16
    input_u16
    input_u16
NODE_INPUT_LIST_END
```

The final element of a node block is its input list. Unlike the node ID and coordinates, the input list is delimited by a pair matched tags, `NODE_INPUT_LIST_START` (4) and `NODE_INPUT_LIST_END` (-4). Between these tags is simply a list of escaped `u16`s. These are zero-indexed indices of the broader node section, each representing an input for the node. Disconnected inputs have a special value of 65535. All inputs must be escaped with a skip tag. Usually, this will take the form of a `SKIP_U8` just inside the node input list block. To skip all inputs, the value of the `SKIP_U8` should be equal to the number of inputs multiplied by 2 as each input (`u16`) takes 2 bytes. Alternatively, an implementor may simple insert a `SKIP_2` tag before each input:

```ignore
NODE_INPUT_LIST_START
    SKIP_2 input_u16
    SKIP_2 input_u16
    SKIP_2 input_u16
NODE_INPUT_LIST_END
```
