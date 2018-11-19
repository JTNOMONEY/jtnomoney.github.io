---
layout: post
title:  "Install embedded rootfs on USB disk"
date:   2018-11-19 16:46:10 +0800
categories: Linux
---

USB disk preparation
---
Prepare a USB disk and format to EXT4 filesystem on host PC (my env is Ubuntu 16.04)
{% highlight shell %}
fdisk /dev/sdb
#use fdisk to format usb and partitioning USB what you want
mkfs.ext4 /dev/sdb
#you need to double check which /dev/sd? is detected, example: sdb
{% endhighlight %}

Rootfs generation
---
Use debootstrap to make a debian rootfs, check[1]
or refer to a good scripts on github[2]

{% highlight shell %}
sudo ./make-rootfs.sh armel
#armel should be general on arm platform; 
#armhf is also supported but you need to check your target board with FPU
{% endhighlight %}

{% highlight shell %}
sudo cp -rvf debian-rootfs/build/armel/armel-rootfs-2018xxxx /media/jt/xxxx/
#Copy generated rootfs folder to USB where it was mounted
{% endhighlight %}


Generated a chroot script
---
Wrote a chroot script (chrootfs.sh) and stored into USB disk

{% highlight shell %}
#!/bin/busybox sh

chroot="/mnt/disk1/armel-rootfs"
bin="/bin/bash"
usb="/dev/sda"

bb="/bin/busybox"

if [ ! "x$1" = "x" ]; then
        bin="$1"
fi

$bb mkdir -p "${chroot}/dev"
$bb mkdir -p "${chroot}/proc"
$bb mkdir -p "${chroot}/sys"
$bb mkdir -p "${chroot}/bcmfs"

$bb mount | $bb grep -q "${chroot}/dev"     || $bb mount -o bind /dev     "${chroot}/dev"
$bb mount | $bb grep -q "${chroot}/dev/pts" || $bb mount -o bind /dev/pts "${chroot}/dev/pts"
$bb mount | $bb grep -q "${chroot}/proc"    || $bb mount -o bind /proc    "${chroot}/proc"
$bb mount | $bb grep -q "${chroot}/sys"     || $bb mount -o bind /sys     "${chroot}/sys"
$bb mount | $bb grep -q "${chroot}/bcmfs"   || $bb mount -o bind /        "${chroot}/bcmfs"

export PATH="/usr/local/bin:/usr/local/sbin:/usr/sbin:/sbin:/usr/bin:/bin"
export HOME="/root"
export USER="root"

$bb chroot "$chroot" "$bin"
{% endhighlight %}


Chroot on target board
---
Install USB disk on target board and execute chroot scripts
{% highlight shell %}
./chrootfs.sh
{% endhighlight %}


Install utility via apt package
---
{% highlight shell %}
apt-get update
#please check your networking before accessing apt package.
apt-get install python
#install python as example

{% endhighlight %}

Reference
---
[1] https://wiki.debian.org/EmDebian/CrossDebootstrap

[2] https://github.com/jubinson/debian-rootfs


