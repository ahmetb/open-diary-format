# Diary Media Attachments Specification

![](http://cl.ly/image/0b323q2v1t2J/diary.jpg) 

_What good is a diary if you can't stick photos on pages?_

Media attachments are a good way to enrich diary entries. Users should be able to freely attach photos, videos, audio recordings or other sorts of convenient media types to their diary entries.

## Media Types

This spec should define a minimum set of media types every diary keeping app should support (both attaching and viewing).

Media types can be extended to store different types of data (e.g. metadata) about days as a part of the diary; however they should not turn the diary a personal database –it is simply not meant for that.

Media is supposed to enrich the diary entry content with more memorable things about that day.

Media types are **identified by their file extensions**. An application should do its best to figure out which media attachments it can show. It is best to use standard, open and convenient media formats while attaching media.

* **Audio:** Meant to be used for voice recordings and memos. User may sometimes choose to just record a voice rather than writing a long entry. TODO: Find out common audio formats recorded and played by current popular devices.
* **Image:** Meant to be used for photos. As of this writing, supporting media/jpeg (.jpg, .jpeg) makes sense as most digital cameras and phones store photos in this format. EXIF-like metadata must be preserved if there's any.
* **Video:** Similar to images, should support open and popular formats which have widespread use. Supporting MPEG-4 (video/mp4) or WEBM (video/webm) makes sense as most mobile devices and browsers support these as of this writing.

An application should do its best to use an open and standard format that will remain in use for a long time. If not possible, the application can just go and use the media format applicable to its platform.

## Attaching Media

Before attaching any media to a diary entry, a diary entry file must exist with the date, even though it's empty.

File name for media attachments should be in the following format: `YYYY-MM-DD-IDENTIFIER.EXTENSION`. For example: `2015-01-05-1.jpg`, `2015-01-05-Voice Recording (01).wav`.

Please note the IDENTIFIER segment is compulsory. There should not be an attachment like `2015-01-05.JPG`. This restricts apps from figuring out if this is a diary entry or media attachment. For the sake of privacy, diary-keeping apps can use a random string for IDENTIFIER rather than revealing what the attachment is about.

This will:

* ...make it easy to load attachments existing for a day.
* ...will keep the attachments for a day close to each other in a listing.

Media attachments will go the the same folder the diary entry file goes –the month directory (see Diary Layout Specification).

This will:

* ...list the attachments for a day in the same request to the filesystem to list the diary entries.
* ...make it easy to manually new attachments directly by going into the datastore.

There is no order for attachments and apps can choose their own method to sort the attachments for displaying. As a rule of thumb, sorting by modification date in ascending order might be useful for users as it reflects the addition date.

### Example Media Layout

	2015/
	└── 01/
	    ├── 2015-01-04.md
	    ├── 2015-01-05-DSC_6568.JPG
	    ├── 2015-01-05-DSC_6569.JPG
	    ├── 2015-01-05-Video 568.mp4
	    ├── 2015-01-05.md
	    └── 2015-01-06.md
    
In the example above, entry for 2015-01-05 has three attachments: 2 pictures and 1 video.

## Encryption

Media attachments should be encrypted the same way the entry is encrypted. The same encryption algorithm and keys should be used for the entry as well as its attachments.

TODO: Update when encryption spec is ready.

## Extending Media Attachments

##### Location

It might be handy to specify location (as coordinates or city name etc.) where the diary entry is written.

TODO: see if open GeoJSON format can be utilized here.