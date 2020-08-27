
---
title: "Transcoding"
date: "2010-01-17T11:08:00-04:00"
draft: false
---

Been messing with HandBrake a lot lately to transcode the majority of my movie/anime library into an encoding the xbox360 can understand. It's a great program; very easy to use thanks to "presets", a set of configuration options to the encoder and muxer to encode the video the way you want. It understands pretty much any format, including straight DVD rips, but with the latest version it only outputs to a few modern formats. xvid, ogm, and dvix have all been deprecated, but since the developers of those codecs are nowhere to be found anymore, I can understand their decision making.

$ for i in `seq -w 25` ; do HandBrakeCLI -Z Normal -i Darker_Than_Black_$i*.mkv -o darker_than_blacker-$i.avi ; done

That command will keep my computer busy for a while. It transcodes the entire Darker Than Black series using the Normal preset, one that the xbox360 understands and keeps much of the quality & compression with its use of x264 codecs. It also works in parallel, so all 4 cores are busy cooking away. It'll take about 4-5 hours to complete transcoding this series. Next up will be 4 seasons of Futurama.

If HandBrake didn't have presets, that command would look like this:

$ for i in `seq -w 25` ; do HandBrakeCLI -e x264 -q 20.0 -a 1 -E faac -B 160 -6 dpl2 -R 48 -D 0.0 -f mp4 --strict-anamorphic -m -x ref=2:bframes=2:subme=6:mixed-refs=0:weightb=0:8x8dct=0:trellis=0 -i Darker_Than_Black_$i*.mkv -o darker_than_blacker-$i.avi ; done

... which means it's time to use a tool with a GUI to handle that mess. But HandBrake fixes that quite well. (and there is a GUI version of it for Windows) One easy shell command to transcode entire tv series at a time? Yes please.
