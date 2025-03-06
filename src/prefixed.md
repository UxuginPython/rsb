# Prefixed Information

The layout of an RSB file at its most basic level is "magic numbers - version - tag tree." The tag tree is discussed more thoroughly in the [next chapter](tree.md).

## Magic Numbers

At the beginning of every RSB file, the UTF-8 string `rrtkstrmbldr` appears.

## Version

Immediately following the magic numbers, the RSB specification version appears. It is formatted as four `u8`s, usually called 'major,' 'minor,' 'patch,' and 'pre.' The first three are identical to the major, minor, and patch components of the specification's [semi-semantic version](versioning.md). The 'pre' strays from strict semantic versioning however: Instead of matching one of its numbers, it begins at 0 with the first prerelease and increments by 1 with each subsequent one, regardless of whether it's an alpha, beta, or something else. It is always equal to 255 in stable versions.
