# Introduction
This document is a series of notes, commands, code snippets, and other bits of information that I have found useful during my time using OpenBSD.
Most of the information in this document is stolen from mailing list archives, reddit (unfortunately), various forums, OpenBSD's FAQ, and DuckDuckGo searches.
If something is listed in this document it is because I personally found it useful, and it is my hope that someone else may too find it useful.
This will continue to be updated as time goes on.

You can download OpenBSD from any of these mirrors:
- https://www.openbsd.org/ftp.html

The FAQ is a great place to start if you're looking for more information on getting started with OpenBSD:
- http://www.openbsd.org/faq/index.html

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
