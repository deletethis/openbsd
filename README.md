# Introduction
This document is a series of notes, commands, code snippets, and other bits of information that I have found useful during my time using OpenBSD.

You can download OpenBSD from any of these mirrors:
- https://www.openbsd.org/ftp.html

The FAQ is a great place to start if you're looking for more information on getting started with OpenBSD:
- http://www.openbsd.org/faq/index.html

I recommend using the -current branch of OpenBSD for daily drivers and workstations.
- http://www.openbsd.org/faq/current.html

## Miscellaneous

### Xenodm
```
vi /etc/X11/xenodm/Xsetup_0
```

```
#!/bin/sh
# $OpenBSD: Xsetup_0.in,v 1.1 2021/08/30 15:38:27 matthieu Exp $

prefix="/usr/X11R6"
exec_prefix="${prefix}"

# ${exec_prefix}/bin/xsetroot -fg \#6f6f6f -bg \#bfbfbf -bitmap ${prefix}/include/X11/bitmaps/root_weave

xsetroot -solid black

# ${exec_prefix}/bin/xconsole -geometry 480x130-0-0 -daemon -notify -verbose -fn fixed -exitOnFail

#  install package openbsd-backgrounds
#  then uncomment:
#
# if test -x /usr/local/bin/openbsd-wallpaper
# then
#       /usr/local/bin/openbsd-wallpaper
# fi

# sxpm OpenBSD.xpm &
```

### Setup Doas
```
echo -e permit nopass $USER >> /etc/doas.conf
```

## Multimedia

### Enable Audio and Video Recording
```
chown $USER /dev/video1
sysctl kern.audio.record=1
sysctl kern.video.record=1
echo kern.video.record=1 >> /etc/sysctl.conf
echo kern.audio.record=1 >> /etc/sysctl.conf
```

### Recording Audio and Video

#### Record Audio
```
aucat -o file.wav
```

#### Record Screen
```
ffmpeg -f x11grab -s 1366x768 -r 30 -i $DISPLAY -c:v libx264 -preset ultrafast ~/Videos/file_name.mkv
```

#### Record Webcam
```
ffplay -f v4l2 -input_format mjpeg -video_size 1920x1080 -i /dev/video1
```
