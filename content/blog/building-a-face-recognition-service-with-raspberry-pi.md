---
title: "Building a Face Recognition service with Raspberry Pi"
date: "2018-05-17"
cover:
  image: "/images/blog/raspberry-camera.jpeg"
summary: "This post is about building your own Raspberry Pi face recognition service."

---

Hey guys,

This post is about building your own Raspberry Pi face recognition service.

Hardware prerequisites:

\- A working Raspberry Pi (I've used model 3+, the fastest on the market at the time of writing this article) with a 2.5A charger, a 16 Gb SD-card, HDMI cable - Any USB webcam - Optional: an Arduino like [motion sensor](http://www.mpja.com/PIR-Motion-Detector-for-Arduino/productinfo/31227+SC/)

**Note**: this setup might work on older versions of the Pi, however the overall performance might be impacted!

Software prerequisites:

\- You will need latest version of [Raspbian](https://www.raspberrypi.org/downloads/raspbian/) installed on the Pi - WiFi or Ethernet working and configured to your local network.

Run `sudo raspi-config` and configure the basics: - Set up your keyboard layout (It defaults to a British keyboard layout) - Change default user password - Enable the Raspberry Pi camera (if you have one attached) - Configure gpu memory split under 'Advanced'. Set it up '16'. - Save changes and reboot.

Install required libraries with these commands:

`sudo apt-get update sudo apt-get upgrade sudo apt-get install build-essential \ cmake \ gfortran \ git \ wget \ curl \ graphicsmagick \ libgraphicsmagick1-dev \ libatlas-dev \ libavcodec-dev \ libavformat-dev \ libboost-all-dev \ libgtk2.0-dev \ libjpeg-dev \ liblapack-dev \ libswscale-dev \ pkg-config \ python3-dev \ python3-numpy \ python3-pip \ zip sudo apt-get clean`

Install the picamera python library with array support (if you are using a camera): `sudo apt-get install python3-picamera sudo pip3 install --upgrade picamera[array]`

Temporarily enable a larger swap file size (so the dlib compile won't fail due to limited memory):

`sudo nano /etc/dphys-swapfile`

< change CONF\_SWAPSIZE=100 to CONF\_SWAPSIZE=1024 and save / exit nano >

`sudo /etc/init.d/dphys-swapfile restart`

Download and install dlib v19.6:

`mkdir -p dlib git clone -b 'v19.6' --single-branch https://github.com/davisking/dlib.git dlib/ cd ./dlib sudo python3 setup.py install --compiler-flags "-mfpu=neon"`

Install face\_recognition:

`sudo pip3 install face_recognition`

Revert the swap file size change now that dlib is installed:

`sudo nano /etc/dphys-swapfile`

< change CONF\_SWAPSIZE=1024 to CONF\_SWAPSIZE=100 and save / exit nano >

`sudo /etc/init.d/dphys-swapfile restart`

Download the face recognition code examples:

`git clone --single-branch https://github.com/ageitgey/face_recognition.git`

**Last step! Running our stuff!** `cd ./face_recognition/examples python3 facerec_on_raspberry_pi.py`

Totally Optional: If you want a desktop GUI, install PIXEL:

`sudo apt-get install --no-install-recommends xserver-xorg xinit raspberrypi-ui-mods`

Once you run the script, the end result should look something like this:

![](images/face_detection_requests_obama-300x205.jpg)

Thanks to [Adam Geitgey](https://github.com/ageitgey) for creating his really nice Python library, which you can find in his Github account.
