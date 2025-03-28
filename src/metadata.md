# Metadata

Besides the node section, the tag tree can contain other information about the file that is not specific to any one node.

## `RRTK_TARGET_VERSION` (6)

```ignore
RRTK_TARGET_VERSION SKIP_4 major_u8 minor_u8 patch_u8 pre_u8
```

The version of RRTK that the generated code is intended for. This version is formatted in the same way as the RSB specification version at the beginning of the file (major - minor - patch - pre). Unlike the specification version however, the RRTK target version must be escaped with skip tags. A single `SKIP_4` is strongly recommended.

## Library Name Tags

```ignore
LIBRARY_NAME_START SKIP_U8 (length - 1)u8 library_name LIBRARY_NAME_END
```

The matched pair of tags `LIBRARY_NAME_START` (9) and `LIBRARY_NAME_END` (-9) are used to delimit the UTF-8-formatted name of the library implementing a version of this specification that last wrote the file. The contents of this block must be escaped with skip tags. Using `SKIP_U8` is recommended.

## Library Version Tags

Unlike with RRTK and the RSB Specification itself, one cannot rely on every implementation of RSB using semantic versioning (although it is preferred). Thus, the matched tags `LIBRARY_VERSION_START` (10) and `LIBRARY_VERSION_END` (-10) are used to delimit the version of the implementing library. The contents of the block formed by these tags must be escaped by skip tags. Implementors can choose to store their version numbers either textually or in binary format. If storing the version textually, UTF-8 is preferred but not required.

## Extension Information

The matched tags `EXTENSION_INFO_START` (11) and `EXTENSION_INFO_END` (-11) are used to contain information about extensions of the RSB specification. The contents of the block formed by these tags must be escaped by skip tags, but besides that, there are no requirements as to what the block contains. Multiple extension information blocks are allowed. There are very few hard requirements for specification extensions (and there cannot be, since the original has no real control over its modifications), but there are a few guidelines to keep things running smoothly compatibility-wise.

### Specification Extension Guidelines

- Have some way of identifying which extension information block(s) belong to your extension. Others may be present.
- Use one and only one extension information block per specification extension. This is not as big of a deal if you follow the above.
- Obviously, don't break compatibility with the original version of the RSB specification.

## Comment Tags

```ignore
COMMENT_START SKIP_U8 (length - 1)u8 comment COMMENT_END
```

The matched tags `COMMENT_START` (12) and `COMMENT_END` (-12) are used to delimit UTF-8 human-readable comments about the file. The contents of the block formed by these tags must be escaped with skip tags. There should be only one comment block in each file.
