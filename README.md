# exaf

The EXtensible Archiver Format to be used in compressing and archiving files. It is intended to be an alternative to the well-known zip and 7-zip formats, with extensibility in mind, as well as trying to avoid the shortfalls of said formats.

**This is a work in progress.** Thoughts and critiques are welcome, so if after reading all of this you have any comments or criticisms, please do not hesitate to share them by filing an issue. Thank you.

## Specification

A proper one is coming soon, once the proof of concept is finished.

If you can read an emacs [org-mode](https://orgmode.org) file, check out the `TODO.org` file for the file format as it exists currently.

In short, it takes inspiration from both [xar](https://en.wikipedia.org/wiki/Xar_(archiver)) and [Exif](https://en.wikipedia.org/wiki/Exif) in that there is a basic header at the start of the file which identifies the format and version, followed by zero or more optional tag/value pairs akin to Exif or the zip format's "extra fields" as described [here](https://en.wikipedia.org/wiki/ZIP_(file_format)). While the archive header may not have any of these optional tags, the directory and file entries within the archive will consist entirely of these rows of data. This makes nearly all metadata for directories and files optional, such as the user and group that own the file or the last accessed time.

## Objectives

For now, complete the proof of concept by building an `exaf` binary that can pack and unpack archives with a modest amount of functionality.

Eventually the purpose of this project will be to provide both format specification and a binary (`exaf`) that will pack and unpack files into and out of archives. Additionally, a [Rust](https://www.rust-lang.org) library with an interface similar to that of the [tar crate](https://docs.rs/tar/latest/tar/) will be published.

Features will ultimately include the following:

* Versioned format specification that dictates what features are required for compliant applications and libraries.
* Archiving many files and their directory structure.
* Compression that is not limited to one particular algorithm.
* Optional encryption of both file data as well as the directory and file metadata.
* API for packing arbitrary data, not just files stored on disk.
* Extensibility first and foremost to promote a future-proof design.

## Build and Run

### Prerequisites

* [Rust](https://www.rust-lang.org) 2021 edition

### Instructions

For the time being there are no unit tests, so simply build and run like so:

```shell
cargo run
```

## Prior Art

There are [many existing](https://en.wikipedia.org/wiki/List_of_archive_formats) archive formats, many of which have long since fallen out of common use. Those that remain are not without their shortcomings, such as poorly implemented encryption features, or vulnerability to compression factor exploits (*zip bomb*).

The original motivation to start this project began when O announced the [pack](https://pack.ac) file format. They introduced a novel approach to the problem of archiving and compressing files while lamenting the general lack of progress in this area. After finding out about the Xar format, the idea for this file format started to take form. XML is neat because it's humanly readable but it's hardly compact, and the massive tree structure at the beginning of the file makes producing, or modifying, an archive rather challenging.

## References

* [7-Zip](https://www.7-zip.org)
* [Exif](https://en.wikipedia.org/wiki/Exif)
* [tar](https://en.wikipedia.org/wiki/Tar_(computing))
* [xar](https://en.wikipedia.org/wiki/Xar_(archiver))
* [zip](https://en.wikipedia.org/wiki/ZIP_(file_format))
