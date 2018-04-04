# Running CV on a NVIDIA Jetson ("Tegra")

To install OpenCV 3.0, you can run [this
scipt](https://github.com/Team694/stuyvision-lib/blob/master/install-opencv-jetson.sh)
from stuyvision-lib:

```
$ ./install-opencv-jetson.sh
```

Again, make sure to install the dependencies.

**Note!** It may be better to use the OpenCV that the Jetson comes with.  See
[this part](https://youtu.be/bsuZq1mvwio?t=19m14s) of Team 195's talk.

## Running your code on startup

To run your code automatically when the Tegra boots, you can set up a
runlevel. Most Linux machines have 7 runlevels, numbered 0 through 6,
in which 0 shuts down the system, 6 reboots, and 1 through 5 startup
the machine in various different ways. You can read more about runlevels
[here](https://en.wikipedia.org/wiki/Runlevel) and
runlevels in Debian in particular [here](https://wiki.debian.org/RunLevel).

We will show setup of runlevel 4, a runlevel open for customization in Debian
and LSB (Linux Standard Base)-compliant distributions.

What will run in runlevel 4 is determined by the contents of `/etc/rc4.d/`.
This directory contains symbolic links to the scripts that will run when
booting to this run level.

Add a symbolic link to a script which will run your code.  Give it a name
beginning with `S`, followed by a two-digit number, and then a descriptive
name. The two-digit number determines the order in which the scripts will run.

E.g.:

```
$ vim /path/to/script # Write all that scripty goodness
$ cd /etc/rc4.d/
$ sudo ln -s /path/to/script S80run-cv
```

An example startup script can be seen
[here](https://github.com/Team694/stuy-vision-2016/blob/master/run-cv.sh).

**In order to set runlevel 4 as the default runlevel**, open
`/etc/init/rc-sysinit.conf`

Find the line `env DEFAULT_RUNLEVEL=2`, and change it to

```
env DEFAULT_RUNLEVEL=4
```
