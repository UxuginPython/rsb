# Specification Versioning

Specification versioning for RSB roughly matches [Semantic Versioning](https://semver.org/spec/v2.0.0.html). An increase in minor version must not break backwards compatibility with the specification. In other words, a file generated based on specification version 1.1.0 must still be valid in version 1.0.0, although some features may not be present. A program based on 1.0.0 should be able to open a 1.1.0 file but should alert the user that not all features of the file may be usable and that they could be lost upon saving. How programs determine the specification version of a file will be explained in [the next chapter](format.md#version).

Major version increases do not have this requirement. A 2.0.0 file does not need to be valid in 1.0.0, and programs based on 1.0.0 should refuse to open it.

Patch versions, of course, should be very minor in their scope and should not add any new features. These versions are only for clarification, and ideally the actual content of files should not change between patch versions. Guidelines for how programs should treat files of mismatched patch version depend on the version's content, but patch version should generally be able to be mostly ignored.

Prerelease version information should be mostly treated like the patch version but a bit more volatile.

## Opening a file of an older major or minor version

If possible, programs should alert the user of the version difference and provide two options:

1. Convert the file to the latest version. If a difference in major version, **programs should make it clear that this means that the program with which the user previously saved the file will no longer work.** Having an interface for creating a backup is strongly recommended.
2. Run in a "compatibility mode" with features from newer versions disabled. Save in the file's existing version. This may be desired even with only a difference of minor version to prevent the following from occuring:
    1. The user creates the file in a program based on 1.0.0.
    2. The user opens the file in a program based on 1.1.0 and converts the file, assuming that the original program will still work correctly.
    3. The user opens the file in the original program again, only to discover that everything 1.1.0-specific has disappeared.

    or, even worse,

    3. The user opens the file in the 1.0.0 program and doesn't see anything odd about newer features missing. The user saves the file and assumes that newer features in the file will be carried over.
    4. The user discovers in the newer program that previous work done there is lost.

Programs may also add a third option for the case of a major version difference:

3. Convert the file to the latest minor version matching the file's existing major version, and then run in the compatibility mode for that version. **Programs should make it clear that, although the previous program will still be able to read the file, it will likely not be able to save it without loss of more recently added features.** A backup interface is not necessary here because the file can still be read by the older program.

Here's a summary of what these options mean:
|Option|Reading Preserved|Writing Preserved|
|------|-----------------|-----------------|
|1     |No               |No               |
|2     |Yes              |Yes              |
|3     |Yes              |No               |

"Reading Preserved," obviously, means that programs based on the file's existing version will still be able to read it. "Writing Preserved" means that programs based on the file's existing version can additionally still write to it without loss of information added by a program of a newer version; the scenario described in option 2 cannot occur.

## Opening a file of a newer minor version

Programs opening a file of a newer minor version can really only provide a single option: Offer to create a backup, open the file as though it were of an older version, and confirm that the user is OK potentially losing some information added by the newer version before saving. **It is very important that programs do not save in an older version without either creating a backup or confirming with the user first.**
