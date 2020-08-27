
---
title: "Stream Ripping"
date: "2010-04-02T11:22:00-04:00"
draft: false
---

Wednesday Illinoise implicitly told me he installed Fedora on his new system, so this post is a tribute to him as a reminder why Linux is more fun to work with for the hobby programmer. I tried to be pedantic and thorough so everyone can follow along. Consider this command:

ffmpeg -i $(find ~/.mozilla -regex '.*Cache.*' -a -not -regex '.*_CACHE_.*' -printf '%T+ %p\n' | sort -n | cut -f2 -d' ' | xargs file | grep -i Video | awk -F : '{ print $1 }' | tail -1) -vcodec msmpeg4v2 -b 1024000 -ab 128 -s 640x480 video.avi

As most of us know, when watching a video on the internet that video has to be stored somewhere on your system so the codec can process it. That location is in the browser cache. That line makes two assumptions: you have ffmpeg installed (trivial to do), and you use Firefox, or some Mozilla-like browser. From start to finish, that line does this:

* find ~/.mozilla -regex '.*Cache.*' -a -not -regex '.*_CACHE_.*' -printf '%T+ %p\n': In the ".mozilla" directory, return a list of all file paths that have "Cache" but not "_CACHE_" in it. Print them with their last modification date and the path. An example would be "2010-04-02+08:35:36.2555301030 /home/jgreguske/.mozilla/firefox/xbskw29l.default/Cache/A927CCE4d01.
* sort -n: Sort that listing numerically. Now our list goes from oldest cached file (any file in the browser cache) to newest.
* cut -f2 -d' ': Only take the second field of that listing. At this point we have a listing of cached files in chronological order. (the modification date has been stripped off)
* xargs file: for every entry, pass it in as an argument to the "file" command. This tells us more about the file. In Windows you have the file extension to do that (.exe means executable, for example). In Linux there is no such convention for the most part, so the "file" command exists to tell us about it. Example output of file looks like this: "/home/jgreguske/.mozilla/firefox/xbskw29l.default/Cache/A927CCE4d01: GIF image data, version 89a, 524 x 494". So at the end of this step we have a list of lines like that.
* grep -i Video: Presumably at least one of the cached files we have is a video. The file command will tell us that by describing it as "Video". Grep is a common Linux command that when given a list of text data, will filter out lines with a particular piece of text in it. In this case that piece of text is "Video", so now we have a list of entries only for video files.
* awk -F : '{ print $1 }': Looking at the example earlier this command will only take the first field (/home/jgreguske/.mozilla/firefox/xbskw29l.default/Cache/A927CCE4d01:) and cut off the colon. It does this for every entry. What we're left with is a list of video files in chronological order.
* tail -1: Take the bottom entry in the listing only. That is the most recent cached video file.
* ffmpeg -i $() -vcodec msmpeg4v2 -b 1024000 -ab 128 -s 640x480 video.avi: All of that work is substituted into the space between the $( and ) in the first line. So the command that is actually executed looks something like this: ffmpeg -i /home/jgreguske/.mozilla/firefox/xbskw29l.default/Cache/A927CCE4d01 -vcodec msmpeg4v2 -b 1024000 -ab 128 -s 640x480 video.avi. This takes that file and transcodes it into an mpeg4 video with 1Mbit video rate, 640x480 resolution and 128Kbit audio, and saves it as video.avi. These last few options might have to be tweaked if you're watching something HD or really low quality.

So there you go, a one-line command to yank out cached videos from your browser and save them locally. Yes, this is what I do on my days off. Works on youtube and most likely your favorite porn site. Enjoy.

Thanks to Art Blakey, whose jazz kept me motivated
