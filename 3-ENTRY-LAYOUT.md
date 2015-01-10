# Diary Entry Specification

Diary entries are supposed to contain the entry contents.

### Entry File Formats

Users should be able to use their choice of markup language to store their entries.

However there should be a minimum set of standard formats which can be rendered and edited on applications implementing the spec.

The entry file format can be inferred from the file extension of the entry file (see Diary Layout Specification document for entry file names).

The formats should be the ones commonly known and easily used. Recognized formats are:

* **txt**: plain text
* **md**, **mdown**, **markdown**: [CommonMark](http://commonmark.org) (strongly specified Markdown)

Inferring the file format from file extension should be done in case-insensitive manner.

### Entry File

1. Entry file should only contain the content the diary author is going to write.

1. If the diary is stored as encrypted, the file should only have the encrypted contents of the entry written by the user.

1. No metadata about the entry should be stored in file contents, file properties or such.

1. User should be able to use Unicode (UTF-8) characters in the entry file. Such characters should be stored and rendered correctly.

1. File modification time (mtime) can be used to reflect the last edit made to entry file. This is not required and is only for user to keep track.

### Example Entry File

> Filename: 2015-01-01.md

```
Today was _really_ fun! We went to Ocean Beach with friends and got some sun tan. 🐳

I should probably do this more! 🐒
```
