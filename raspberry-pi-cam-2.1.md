# Raspberry Pi -- Camera 2.1

[The Cam](https://www.raspberrypi.org/products/camera-module-v2/).

![The Cam](img/Pi-Camera-attached-1-480x384.png)

- Sony IMX219 Exmor R back-illuminated 8-megapixel sensor
- 1080p30, 720p60 and VGA90
- CSI bus, MMAL and V4L APIs
- Made by [Element 14](https://www.element14.com/)
- [Getting Started with the Pi-Camera](https://www.element14.com/community/docs/DOC-65138/l/getting-started-with-the-pi-camera-instructions)

- The First image taken using `raspistill -o pic1.jpg`:  
![The First Image Taken](img/pic1.jpg)
- The First video taken using `raspivid -o vid1.h264`: [The First Video Taken](img/vid1.h264)

## System Tools

- [Configuration tool for the Raspberry Pi](https://github.com/RPi-Distro/raspi-config)
- [element14/Raspberry Pi Project](https://github.com/element14/pi_project)

## Assorted TFMs

- [HOWTO - Create a Raspberry Pi IP Camera with RTSP server](https://random-notes-of-a-sysadmin.blogspot.ru/2015/05/howto-create-raspberry-pi-ip-camera.html) using **live555** libs.  
Ends in `raspivid -t 0 -fps 30 -g 1 -b 2000000 -h 1920 -w 1080 -o - | ./testRaspi`.
- [picamera](http://picamera.readthedocs.io/) Python APIs and other stuff worth to read.

# EOF #
