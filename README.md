# Introduction
This document is a series of notes, commands, code snippets, and other bits of information that I have found useful during my time using OpenBSD.

You can download OpenBSD from any of these mirrors:
- https://www.openbsd.org/ftp.html

The FAQ is a great place to start if you're looking for more information on getting started with OpenBSD:
- http://www.openbsd.org/faq/index.html

I recommend using the -current branch of OpenBSD for daily drivers and workstations:
- http://www.openbsd.org/faq/current.html

## Miscellaneous

### Setup Doas
```
echo permit persist $USER > /etc/doas.conf
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

#### Activate Webcam
```
ffplay -f v4l2 -input_format mjpeg -video_size 1920x1080 -i /dev/video1
```

#### Record Screen
```
ffmpeg -f x11grab -s 1366x768 -r 30 -i $DISPLAY -c:v libx264 -preset ultrafast ~/Videos/video.mkv
```

#### Record Audio
```
aucat -o ~/Videos/audio.wav
```

#### Merge Audio/Video
```
ffmpeg -i video.mkv -i audio.wav -c:v copy -c:a aac output.mp4
```

