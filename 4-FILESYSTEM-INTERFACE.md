# Filesystem Interface

This specification explains what properties and functions are expected from filesystems or bridge implementations for a filesystem or a storage media.

## Expected Properties and Functions

1. **List Directory:** returns list of directory and file names in a directory.

1. **Create Directory:** Should be able to create a directory if not exists.

1. **Write File:** Saves given byte array (blob) to the file at the specified path. Creates the file if it does not exist.

1. **Delete File:** Deletes given file at the specified path.

1. **Get File:** Downloads content of a given file at the specified path.

### Case sensitivity

Some filesystems are case-sensitive (commonly on Linux and Mac OS filesystems) and some are not (Windows filesystems). Worse, a cloud file storage system which synchronizes files between Linux and Mac filesystems usually poorly handle the files with same names using characters from different cases.

It's best to avoid these issues by not using case-sensitive comparisons. If a file is read, it should be saved with the exact same name.

## Implementations

It is suggested for every diary keeping application to implement supported filesystem wrappers separately. For example, web app should provide implementations of the filesystem interface for local fs, Dropbox etc. and iOS app should implement Dropbox, Google Drive, OneDrive etc.

The rough interface expected from a filesystem implementation along with a full test suite is specified below.

## Filesystem Test Suite

Given the following calls are implemented:

* `ListDir(dirPath)`
* `MkDir(dirPath)`
* `WriteFile(dirPath, fileName, bytes)`
* `DeleteFile(dirPath, fileName)`
* `GetFile(dirPath, fileName)`

The following tests should be satisfied:

* TODO