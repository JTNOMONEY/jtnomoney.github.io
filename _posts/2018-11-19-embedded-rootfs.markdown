---
layout: post
title:  "Install embedded rootfs on USB disk"
date:   2018-11-19 16:46:10 +0800
categories: Linux
---

USB disk preparation
---
Prepare a USB disk and format to EXT filesystem on host PC.
Before formating/partitioning USB disk, you need to double check which /dev/sd? is detected.
In my case, my host PC is using ubuntu 16.04 and inserted USB is detected on /dev/sda.
{% highlight shell %}
fdisk /dev/sdb

mkfs.ext4 /dev/sda
{% endhighlight %}

Rootfs generation
---
Use debootstrap to make a debian rootfs, check[1]. Another good reference is on github[2]. 
To be noticed that 'armel' should be general for arm platform and 'armhf' is advanced and also supported. 
(but you need to check your target board with FPU. See debian website) 
{% highlight shell %}
sudo ./make-rootfs.sh armel
{% endhighlight %}

After you excute the script, rootfs will be put on 'build' folder.
Then, copy generated rootfs folder to USB disk. (In my case, it was on media/jt/xxxx/)
{% highlight shell %}
sudo cp -rvf debian-rootfs/build/armel/armel-rootfs-2018xxxx /media/jt/xxxx/
{% endhighlight %}

Generated a chroot script
---
Prepared a `chroot` script (chrootfs.sh) and stored into USB disk.
Example as below:

{% highlight shell %}
#!/bin/busybox sh

chroot="/mnt/jail/armel-rootfs-2018xxxx"
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
mount /dev/sda /mnt/jail/
{% endhighlight %}

{% highlight shell %}
./chrootfs.sh
{% endhighlight %}


Install utility via apt package
---
Below is a case for example to use `apt-get` and install `python`.
To be noticed that you need to check your networking before using apt package. 
The basic is to check your route gateway and ping 8.8.8.8 for testing.
{% highlight shell %}
apt-get update
apt-get install python
{% endhighlight %}

Reference
---
[1] https://wiki.debian.org/EmDebian/CrossDebootstrap

[2] https://github.com/jubinson/debian-rootfs


