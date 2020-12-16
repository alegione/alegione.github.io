---
title:  "Quick tips for using ffmpeg for video editing"
header:
  teaser: NULL
permalink: "/2020/ffmpegQuickTips"
published: true
comments: true
tags:
  - Unix
  - Education
  - Coding
  - Video editing
---

In this brave new world of 2020, many of us are finding we have to use Zoom or other similar video conferencing software tools to teach classes. Then we wish to take those recordings and quickly edit them to trim, compress, and upload them to an online server. I've found the command line tool **ffmpeg** to be extremely helpful in this endeavour. Below are a few quick commands you can use to get your recording from its raw form in to a final version in just a few commands.



## removed chapters
If you recorded via Zoom into the cloud, then every time you turn screen share on and off, the video adds a 'chapter' marker. This can affect trimming of the video file so it's best to remove chapters immediately.

```
ffmpeg -i video.mp4 -c copy -map_chapters -1 video-noChapters.mp4
```

## trim files at a particular timestamp
It's likely that before the class started you had a few minutes of staring at the screen or getting up to grab a coffee before the other participants arrived. Or perhaps at the end you spoke to a couple of students about things that you don't want the whole class to hear on the recording. To quickly and easily trim bits of the video, you can use the below command. This is trim the first 5 minutes and 11 seconds from the video, and stop it at the 1 hour, 49 minute and 50 second mark.

```
ffmpeg --ss 05:11 --to 01:49:50 -i video-noChapters.mp4 -c copy video-trimmed.mp4
```

**NOTE:** you may find that the first or last 10-30 seconds of the video are missing after this process. That is, the sound will still play, but the video won't be present. This is an issue, from recollection, around frame numbers, so if you trim the video at the wrong time point then the video won't kick in until the next appropriate segment (every 15 seconds for example). Don't worry about this for now, as when you do the re-encoding/compression described below, this missing video will return!

## cut video into sections and concatenate files
Perhaps you had a few sections of class with breakout rooms. You don't want the ten minutes of dead air in your recording, so you want to be able to trim those bits out, then stitch the video back together into one single piece. You could use the following method as an example.

### Trim the video into three sections

```
ffmpeg --ss 05:11 --to 15:20 -i video-noChapters.mp4 -c copy video-part1.mp4
ffmpeg --ss 20:57 --to 40:50 -i video-noChapters.mp4 -c copy video-part2.mp4
ffmpeg --ss 01:08:08 --to 01:49:50 -i video-noChapters.mp4 -c copy video-part3.mp4

```
Now we need to make a text file that contains the names of all the different video files we want to stitch back together. Each file name needs to be preceded by the word 'file', followed by a ' ' (space or tab). Each filename needs to be followed by a new line, with the subsequent file afterwards. The name of the file can be anything you want, I just stick with 'stream.txt' for consistency.

### format for stream.txt text file containing paths for file concatenation

```
file video-part1.mp4
file video-part2.mp4
file video-part3.mp4
```

## Concatenation files
Now we can concatenate our files using the below command:

```
ffmpeg -f concat -safe 0 -i stream.txt -c copy video-Concatenated.mp4
```

## compress a file
The below command should reduce the file size of a recorded Zoom lesson substantially, without reducing the quality too dramatically. This requires 're-encoding' of the video file. The above commands were directly copying the audio and video across, so it was practically instant. For compression the audio and video is adjusted, so it takes significantly longer, and increases with the length of time of the video.

```
ffmpeg -i input.mp4 -vcodec libx265 -crf 28 output.mp4
```

## if you get a stream/packet size error add this before the output statement
```
-max_muxing_queue_size 1024
```
