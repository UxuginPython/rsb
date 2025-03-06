# Tag Tree

RSB uses an XML-like tag system called the "tag tree" for internal organization. This system is designed for both extensibility and backwards compatibility. Unlike XML though, RSB is a binary format. Each tag has a constant `i8` value.

Tags come in two types: matched and unmatched. Matched tags affect everything between an opening and a closing tag. They are generally used for things of varying length or things whose length is likely to change in future versions of the specification. Unmatched tags affect a certain fixed number of bytes after a single tag. They can save a bit of space in some places but are much less extensible, so they are used relatively sparingly.
