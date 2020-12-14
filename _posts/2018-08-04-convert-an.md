---
title: convert android video for youtube via avidemux
author: PipisCrew
date: 2018-08-04
categories: [app]
toc: true
---

-download&install avidemux http://avidemux.sourceforge.net/
-normally the codec of the mobile video is H264 (MP4).with resolution 1920x1080 or more.
-open avidemux > drag drop the sourcevideo.mp4
-goto top menu > video > filters > transform > swsResize
apply this settings, to convert it to **480p**, if you want better resolution use 1280x720 for **720p**.
![snap073](https://www.pipiscrew.com/wp-content/uploads/2016/10/snap073.png)

or use the following for **VGA quality**
![](https://www.pipiscrew.com/wp-content/uploads/2016/10/snap342.png)

-on the side options use the following settings
![snap074](https://www.pipiscrew.com/wp-content/uploads/2016/10/snap074.png)

example
the source filesize is 108mb. After conversion to 480p the filesize is 22mb.

youtube suggested video resolutions - [https://support.google.com/youtube/answer/6375112](https://support.google.com/youtube/answer/6375112)

--
<table>
<tbody>
<tr>
<th>Resolution</th>
<th>Name</th>
</tr>
<tr>
<td>3840x2160</td>
<td>2160p</td>
</tr>
<tr>
<td>2560x1440</td>
<td>1440p</td>
</tr>
<tr>
<td>1920x1080</td>
<td>1080p</td>
</tr>
<tr>
<td>1280x720</td>
<td>720p</td>
</tr>
<tr>
<td>854x480</td>
<td>480p</td>
</tr>
<tr>
<td>640x360</td>
<td>360p</td>
</tr>
<tr>
<td>426x240</td>
<td>240p</td>
</tr>
</tbody>
</table>
All of these resolutions are in the aspect ratio **16:9** widescreen. **Do not** record or create vertical, square, 4:3, or 16:10 video, as it **will have black bars** on the sides when uploaded to YouTube. ([src](https://www.h3xed.com/web-and-internet/youtube-recommended-video-resolutions-for-quality-and-search-optimization))

--

If you are **not quality freak**, encode the video with constant bitrate @ **400kbit**.

![](https://i.imgur.com/KaLgNxQ.png)

**46min** video **854x480** (480p) with **AAC** 128kbps costs only **183mb**

--

Avidemux can by default open the **srt** and **convert** it to **ASS** on the fly, through :

![](https://i.imgur.com/vNhFARB.jpg)

but you **cant** <span style="background-color: #ffff00;">**style**</span> the subs

### Subtitling with ASS

Use the [Aegisub](http://www.aegisub.org/) freeware application. The ASS format defines also the <span style="background-color: #ffff00;">**style**</span> (font + color) of the subtitles.

Open the style manager from the main window, on toolbar click **edit** near the combo, always use **Arial 26**. ([src](http://docs.aegisub.org/manual/Styles))

![](https://i.imgur.com/8rfDlOe.png)

origin - http://www.pipiscrew.com/?p=6145 convert-android-video-for-youtube