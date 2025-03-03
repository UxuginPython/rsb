# General Format

RSB uses an XML-like tag system for internal organization. Unlike XML though, RSB is a binary file format.

The most basic RSB layout is "magic numbers - version - node list."

## Magic Numbers

At the beginning of every RSB file, the UTF-8 text `rrtkstrmbldr` appears.

## Version

Immediately following the magic numbers, the RSB specification version appears. It is formatted as four `u8`s, usually called 'major,' 'minor,' 'patch,' and 'pre.' The first three are identical to the major, minor, and patch components of the specification's semantic version. The 'pre' strays from strict semantic versioning however: Instead of matching one of its numbers, it begins at 0 with the first prerelease and increments by 1 with each subsequent one, regardless of whether it's an alpha, beta, or something else. It is always equal to 255 in stable versions.
