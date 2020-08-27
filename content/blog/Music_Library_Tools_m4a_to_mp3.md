
---
title: "Music Library Tools: m4a to mp3"
date: "2010-07-22T11:27:00-04:00"
draft: false
---

Many songs I have from iTunes are in the m4a format, but since iTunes doesn't exist on Fedora, I have to convert them if I want to listen to them there. I chose mp3 since that is the most interoperable even though it isn't a "free" codec. We start with a simple shell script:

```
if [ -z "$1" ] ; then
    echo 'You must specify a path to an m4a file'
    exit 1
fi

faad -o - "$1" | lame -V 0 - "${1%.m4a}.mp3"
```

Let's note a few things here:

* This script requires lame and faad2. Both can be installed easily via yum.
* This script takes exactly 1 argument: a path to an m4a file.
* Our mp3 will have a variable bit rate using the highest-quality algorithm. I'm a patient guy with a powerful CPU and plenty of HD space, so this is ok. Increase the number to lame's -V if you want something faster at a cost of quality.
* We lose all of the tags and metadata in the conversion. It is possible to get this info and preserve it, but I'm leaving that an exercise to the reader. (all you need is grep and a for loop)

Of course, I'm not going to run this command on every single m4a file. That would take far too much effort an attention; let's add some other shell utils to the mix.

```
find -name '*.m4a' -print0 | xargs -0 -n 1 -P 4 myscript.sh
```

Now we have a solution: that find command returns a list of paths to all files in the current directory that end with .m4a. Each element in the list is null-terminated which is important because we don't want to separate by white-space: some songs have spaces in the file name. xargs does all the heavy lifting for us: it accepts the list from stdin, and executes our little script for each element in the list. -n tells it to append exactly one element to the command, which we need since the script only takes one path at a time. -P tells it to run 4 processes at once, it seemed like a good idea to use all 4 cores in my CPU.

The output was a little funky since 4 processes are competing to print out terminal text, but that can be safely ignored. The xargs logic could be encoded in the shell script instead, but this approach seemed far simpler to me rather than defining a recursive function in the shell script and having to worry about whether a file is an m4a or not.

Next in this series: setting id3v2 tags.

