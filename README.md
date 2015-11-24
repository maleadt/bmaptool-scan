bmaptool-scan
=============

Scan for unallocated blocks in a disk image, and export this information for
further use by `bmaptool`, either by punching holes in the image or by
generating a `bmap` file.



Usage
-----

The script needs quite some Perl packages, which you can easily install using
`cpanm`:

    $ cpanm XML::Writer IPC::System::Simple Number::Bytes::Human Switch Clone

Afterwards, run the script on an image, selecting either `--bmap` or `--sparse`
mode of operation:

    # modprobe loop
    # bmaptool-scan --bmap $FILENAME.img > $FILENAME.bmap

Running the script as root is necessary to `losetup` the image, which also needs
to have the `loop` kernel module loaded.

If you're running the script through `sudo` while using `local::lib`, it is
possible that the `PERL5LIB` variable is scrubbed and packages are not found. A
workaround:

    $ sudo PERL5LIB=$PERL5LIB bmaptool-scan ...



TODO
----

* Add support for partition images (currently only full-disk images containing
  partitions are supported).
* Add support for more file systems.
* Detect funky partition tables (hybrid images, overlapping partitions), and
  abort.
* More robust way of parsing partition table (i.e. don't rely on `fdisk`
  output).
