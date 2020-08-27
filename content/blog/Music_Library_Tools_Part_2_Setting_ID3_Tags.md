
---
title: "Music Library Tools Part 2: Setting ID3 Tags"
date: "2010-08-19T11:33:00-04:00"
draft: false
---

Update: I've made quite a few enhancements to the script:

    Smarter Renaming
    Tags Ogg-vorbis files
    Tags FLAC files
    Handles a few more genres

ID3 tags are bits of data encoded in an mp3 file that catalogue the artist, album, year, genre, song title and other fields of metadata that explain what an mp3 is. On linux, you can manipulate these fields using the id3v2 command line utility. It's important to use version 2 of the ID3 tag specification because modern players skip any tagging done with version 1. Computer trivia: version 1 is encoded at the end of the mp3 file, version 2 is at the beginning. Version 1 supports only ISO-8859-1 string encodings, so international symbols like Kanji are not supported. In fact if you try to use one, you will likely corrupt the mp3. Wikipedia has more info on the subject.

Anyway since id3v2 is a command line utility, I figured I could write a script around it to set all of the id3v2 tags in my mp3 collection appropriately based on their location in the directory tree. My music collection is organized as follows:

music/Genre/Artist/Album

Some mp3s are not sorted, and those are put in "unsorted" directories that may live in the Genre (if I don't know who the artist is) or in an Artist directory (if I don't know what album it is on). The script I came up with skips those directories.

I went with a Perl script since I haven't used Perl in a while, and wanted to keep my skills sharp. There are a couple known issues with it: dollar signs in song titles will confuse it (the Perl interpreter will think they are a variable declaration) and the file name correction subroutine will be incorrect on a few edge cases. ("46 & 2" becomes "and 2" because it thinks it is removing the track number from the start).

Anyway, this script is attached here in the hope that some find it useful. After running it over my entire collection, just about every artist and title is displayed properly in Audacious.
