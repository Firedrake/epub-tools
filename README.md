Roger's tools for ePub

You could probably just use Calibre. If that works for you, great.

Even more than usual, there's no warranty at all on this; I've seen
horrors committed in the name of the supposedly standard ePub, as
always seems to happen when XML gets involved.

* tagepub

Changes author, title, and series information in an ePub file.

Needs Archive::Zip and XML::LibXML.

Usage: tagepub (-a AUTHOR) (-t TITLE) (-s SERIES) (-i INDEX | -I INDEX) EPUBFILE (EPUBFILE...)

If you leave out a parameter, it won't be changed at all. If you
include it, any old entries will be deleted and the new one used to
replace them.

AUTHOR is one or more author names (dc:creator): "Firstname Surname,
Firstname Surname". Use a / to indicate sorting division: "Diana
Wynne/Jones" will insert an opf:file-as attribute of "Jones, Diana
Wynne".

TITLE is the book title (dc:title). If it starts with A, An or The the
software will also set a calibre:title_sort meta field.

SERIES is a series name (calibre:series).

INDEX is an entry number in a series (calibre:series_index).

If you set INDEX with -I, it will be automatically incremented for
each subsequent EPUBFILE.

* kobo-set-series

Sets series information in a Kobo Libra 2 (and probably other recent
Kobo models - tell me if it works for you).

Needs Archive::Zip, XML::LibXML, DBI and DBD::SQLite3.

Usage: kobo-set-series (-p KOBOPATH)

This gets quite fiddly. First of all you need to load the ePubs with
series information into the Kobo. Then disconnect it and allow it to
catalogue the new files. After that, connect again and mount it as a
local filesystem, then run this program. (On Linux the program will
look through /etc/mtab for it; if that doesn't work, or if you're not
on Linux, give the path to the Kobo with -p.)

Once run, your ePubs that are in a series will appear under the
"Series" tab of "My Books", and they'll get a series subtitle in the
main listing.
