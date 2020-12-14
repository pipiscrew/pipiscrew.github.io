---
title: Convert Multiple Videos With Avidemux
author: PipisCrew
date: 2016-02-23
categories: [app]
toc: true
---

reference - [http://www.ehow.com/how_8740523_convert-multiple-videos-avidemux.html](http://www.ehow.com/how_8740523_convert-multiple-videos-avidemux.html)
[http://www.avidemux.org/admWiki/doku.php?id=using:command_line_usage](http://www.avidemux.org/admWiki/doku.php?id=using:command_line_usage)

Create open a batch file aka videoconvert.bat and copy the following text example to use a template for a basic conversion. Note this example is for converting .mp4 video to .avi (Xvid+MP3 encoding) :
```js
set avidemux="C:\Program Files\Avidemux 2.5\avidemux2.exe"

set videocodec=Xvid

set audiocodec=MP3

for %%f in (*.mp4) do %avidemux% --video-codec %videocodec% --audio-codec %audiocodec% --force-alt-h264 --load "%%f" --save "%%f.avi" --quit

(The last two lines should be in one line of text).
```

## Use Joblist

[http://www.avidemux.org/admWiki/doku.php?id=using:joblist&s[]=avidemux&s[]=jobs](http://www.avidemux.org/admWiki/doku.php?id=using:joblist&s[]=avidemux&s[]=jobs)

origin - http://www.pipiscrew.com/?p=3972 convert-multiple-videos-with-avidemux