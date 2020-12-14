---
title: youtube-dl
author: PipisCrew
date: 2020-11-06
categories: [app]
toc: true
---

Is a small command-line program to download videos from YouTube.com and a few more sites. It requires the Python interpreter (2.6, 2.7, or 3.2+), and it is not platform specific.

[http://rg3.github.io/youtube-dl/](http://rg3.github.io/youtube-dl/)

As per 2019.12.25 version and later, using this cmd, selects up to 720p videos with a bitrate of at least 56 KBit/s.
```js
// src - https://github.com/ytdl-org/youtube-dl/blob/master/README.md

// --youtube-skip-dash-manifest - skip DASH items (is only audio OR only video (without audio))
// -f mp4 - force get the best video resolution that is in mp4 format

youtube-dl.exe --youtube-skip-dash-manifest -f mp4 --batch-file list.txt

//or if you want to restrict till 720p (avoid 1080p)

youtube-dl.exe --youtube-skip-dash-manifest -f "(mp4)[height<=720]" --batch-file="" list.txt="" ```=""></=720]">

* * *

example of use :
```js
youtube-dl -f best --batch-file batchlist.txt 

youtube-dl.exe https://www.youtube.com/watch?v=xzZh4fdaUpk --extract-audio --audio-quality 128k

-- all together, convert to mp3 --
youtube-dl.exe --batch-file playlist1.txt --extract-audio --audio-format mp3 --audio-quality 128k

download playlist
youtube-dl -i --extract-audio --audio-format mp3 --audio-quality 128k --yes-playlist "https://www.youtube.com/watch?v=jRGrNDV2mKc&start_radio=1&list=RDGMEMJQXQAmqrnmK1SEjY_rKBGA"

```

* * *

download user videos **contains** specific keyword
```js
// src - https://crackoworld.com/technology-tweaks/how-to-download-youtube-videos-easily/

youtube-dl.exe --youtube-skip-dash-manifest -f "(mp4)[height<=720]" --match-title "morning" https://www.youtube.com/c/yogawithkassandra/videos

```

to convert to mp3, extract near youtube-dl
https://ffmpeg.zeranoe.com/builds/ --match-title="" "morning"="" https://www.youtube.com/c/yogawithkassandra/videos="" ```="" to="" convert="" to="" mp3,="" extract="" near="" youtube-dl=""></=720]" --match-title "morning" https://www.youtube.com/c/yogawithkassandra/videos

```

to convert to mp3, extract near youtube-dl
https://ffmpeg.zeranoe.com/builds/>

origin - http://www.pipiscrew.com/?p=3357 app-youtube-dl