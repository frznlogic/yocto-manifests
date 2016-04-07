yocto-manifests
===============

This repository contain repo tool manifests which can be used to download
everything needed to build specific projects. 


Install repo tool
=================

This is explained in detail at
https://source.android.com/source/downloading.html. The short version is:

```
$ mkdir ~/bin
$ PATH=~/bin:$PATH
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```

FrozenMirror Image
==================

This project builds a yocto jethro distribution for raspberry pi with eglfs and
Qt 5.4 with the FrozenMirror QML project automatically added to the image. To
build, install the repo tool according to the above instructions and follow
these instructions:

```
mkdir ~/frozenmirror
cd ~/frozenmirror
repo init -u https://github.com/frznlogic/yocto-manifests.git -b master -m frozenmirror.xml
repo sync
. setup-environment build
vi conf/local.conf
```

At this point, make sure all the right settings are setup (including if you are
using a raspberrypi1 or raspberrypi2).

```
bitbake -k frozenmirror-image
dd \
if=tmp-glibc/deploy/images/raspberrypi/frozenmirror-image-raspberrypi.rpi-sdimg \
of=/dev/<device> bs=1024
```

Make sure you write the image to a SD card and not your harddrive by accident.
At this point you're done. Plugin the card to your raspberry pi and have a run. 


