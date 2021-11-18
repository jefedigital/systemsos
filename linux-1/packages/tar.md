# tar

archiving utility. (originally ’tape archive’) In Unix and Unix-like systems, archiving and compression are separate.

* tar puts multiple files into a single (tar) file.
* gzip compresses one file (only).

So to get a compressed archive, you combine the two, first use tar to get all files into a single file (archive.tar), then gzip it (archive.tar.gz). If you only have one file you need to compress (notes.txt), there's no need for tar, so you just do gzip notes.txt which will result in notes.txt.gz.

There are other types of compression, such as compress, bzip2 and xz which work in the same manner as gzip (apart from using different types of compression.)

**Format**

tar {A|c|d|r|t|u|x}\[GnSkUWOmpsMBiajJzZhPlRvwo] \[ARG...]

**Flags**

\-c creates a new .tar archive file.

\-x extract / uncompress

\-v verbose mode

\-f file name type of the archive file.

\-z filter through gzip

**Examples**

extract a tar.gz while excluding a specific directory:

tar -xf hadoop.tar.gz --exclude=hadoop-3.2.1/share/doc

Extracting and Repacking .deb files

[https://fabianlee.org/2018/09/28/ubuntu-customizing-and-repacking-a-deb-file/](https://fabianlee.org/2018/09/28/ubuntu-customizing-and-repacking-a-deb-file/)
