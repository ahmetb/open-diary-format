# Diary Layout Specification

## Terminology

To stay sane, the following terminology is used within this specification

##### diary

> a digital book in which one keeps a daily record of events and experiences arranged by date. also known as journal, memoir, chronicle and logbook.

##### entry

> textual log for a day in a diary. only one entry can exist for a day.

##### file system

> the persistent catalog which has notion of directories, sub-directories (directories under directories) and files (data nodes under directories) to store the given data and metadata in the desired layout.
> 
> it can be a physical file system on top of an hard disk (e.g. NTFS) or a filesystem mount that emulates the required properties (e.g. Dropbox, FUSE)

##### storage medium

> the storage system which hosts the file system the diary lives on e.g. hard disk drive, cloud storage, document database etc.

## Layout Definition

Diaries are stored in media that can act like file systems where there is notion of directories, sub-directories and files with names.

* A diary starts with a directory, which gives the diary its name. 
* Each year number is stored as a directory within the root directory.
* Each month number is stored as a directory within that year.
* Entry for each day is stored as a file within that month's directory.
* Entry filename is full ISO8601 date and the extension is the format the entry is written in.

#### Considerations

* Both human and machine readable
* Humans can go to the file system and write new entries manually
* Humans can intervene if anything goes wrong
* Imposes a natural index structure for entries, therefore there is no need for an index file or database that points to where the entries are stored.
* Any application built on top can construct the index from the directory and file layout at a little cost.
* Filenames do not reflect anything about the contents of the entries.
* Having a nested directory structure (rather than flat a directory):
    * makes storage and navigation system scalable by limiting maximum number of entries per level
    * allows apps to discover which years/months exist or not without doing a full scan.
    * limit which days are missing to a single _list files_ call
* Easy migration between storage media (e.g. from flash drive to computer and from there to cloud)
* Easy to back up

#### Example layout

The following directory tree explains the specifications above:

	... file system ...
	├── ... other files ...
	└── Diary
	    ├── 2014
	    │   └── 12
	    │       ├── 2014-12-30.txt
	    │       └── 2014-12-31.txt
	    └── 2015
	        └── 01
	            ├── 2015-01-01.md
	            └── 2015-01-03.md
	            
In the example above:

* diary name is `Diary` and is stored in that folder
* entries exist for years `2014` and `2015`
* 4 entries exist in total
* entries for `2014-12-30` and `2014-12-31` are in plain text format
* entries for `2015-01-01` and `2015-01-03` are in Markdown format
* entry for `2015-01-02` is missing
