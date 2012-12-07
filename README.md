Installation
------------
To install recoverjpeg, run

    ./configure
    make
    sudo make install

To use sort-pictures, you need to install:

  - exif: http://sourceforge.net/projects/libexif
  - ImageMagick: http://www.imagemagick.org/

Usage
-----
Look at the manual pages for recoverjpeg(1), recovermov(1) and
sort-pictures(1).

What to do if the medium is physically damaged?
-----------------------------------------------
Mike Ingle wrote about working with a drive that cannot be read because of errors:

> The hard drive was more complicated because recoverjpeg would abort on the first bad sector it hit.
> I tried using a named pipe and that did not work, so I did:
> 
>    dd if=/dev/sdc of=recovery-image bs=65536 conv=noerror
> 
> and that made an image file while skipping over the bad blocks without aborting. Then I would end up with a
> 500 GByte file which I ran recoverjpeg on, and it worked.

History
-------
recoverjpeg was written on 23 December 2004 after a *huge* mistake:
a disk containing pictures was repartitioned and a new operating
system was installed on top. recoverjpeg and sort-pictures ran on
this 80GB disk and rescued 19222 pictures (11GB):

  - 9538 pictures sorted by date (a few of them were corrupted in a
    way that no software can detect as they are valid JFIF files)
    and taken on 337 different days

  - 1310 JFIF files without date (some of them were correct pictures
    whose exif data had been corrupted)

  - 8301 JFIF files too small to be digital pictures (no error there,
    most of them were thumbnails of real pictures previously made
    by software such as gqview)

  - 71 invalid JFIF files

  - 4 pictures recorded at a date of 0000-00-00 (probably a bug
    in the camera used to take the pictures)

Of course, I had a backup of everything, but I cannot seem to remember
where I put it.

On January 2010, Jan Funke added the recovermov(1) program to the package
to recover lost movies.

On April 2012, Samuel Tardieu added the -d option to recoverjpeg(1) to
circumvent arbitrary limits set on the number of files per directory on
certain limited filesystems. Also, support of compilation with clang(1)
was added.

Portability
-----------
recoverjpeg has been tested on:

  - Arch Linux x86_64 [2010-03-02]
  - Cywgin x86 [2010-03-02]
  - Debian Linux unstable i686 [2010-03-02]
  - FreeBSD 6.2 x86
  - FreeBSD 7.1 x86
  - FreeBSD 7.2 amd64 (Pierre Beyssac)
  - FreeBSD 9 x86 (Pierre Beyssac)
  - FreeBSD 9 amd64 (Pierre Beyssac)
  - Mac OS X 10.6.2 x86_64-apple-darwin [GCC + clang] (Ollivier Robert)
  - NetBSD 5.0.1 x86 (Stéphane Bortzmeyer)
  - NetBSD 5.0.2 x86 (Marc Baudoin)
  - NetBSD 5.0.1 sparc64 (Stéphane Bortzmeyer)

You need to ensure that the off_t type from the C library and the
lseek() function support offsets of at least the size of the device
you want to recover pictures from.

Contact information
-------------------
Home page: <http://www.rfc1149.net/devel/recoverjpeg>

Authors:

  - [Jan Funke](mailto:jan.funke@inf.tu-dresden.de)
  - [Samuel Tardieu](http://www.rfc1149.net/)

Development
-----------
If you got this software using your revision control tool, you can
build the autogenerated files by using:

    autoreconf --install

Thanks
------
The following beta-testers and contributors are warmly thanked:

  - Olivier Beyssac <ob@r14.freenix.org>
  - Pierre Beyssac <pb@eu.org>
  - Bertrand Petit <elrond@phoe.frmug.org>
  - Dunc <dunc@lemonia.org>
