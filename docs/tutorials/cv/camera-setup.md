# Camera setup: getting a (good) image from the camera

## Goal: get a *good* image

Ordinary images are full of useless color.

When targeting bright things like reflexite, your life
is made much easier by setting the exposure, brightness, etc
of the camera. This can black out almost all of the image.

See the left and right images on [this
slide](https://docs.google.com/presentation/d/1KvPWpPO9rFjTZ3nKJy4rmbvxRiOo2EwrciE0fggv8xM/edit#slide=id.g1a472e5d9e_0_47).

### How: Video4Linux2

You can configure LifeCams from a program on Windows, but when its re-plugged in, the settings might not be maintained.

We've used Video 4 Linux 2 (or 'v4l2') to configure the camera. A configuration that we found to be useful is low exposure,
high contrast, and low brightness.

To install v4l2 on the roboRIO, use `opkg`:

```
$ opkg update
$ opkg install v4l-utils
```

For an example, [`setup-camera.sh` in stuyvision-lib](https://github.com/Team694/stuyvision-lib/blob/master/setup-camera.sh)
is a simple script for configuring a camera with v4l2.

Note: you can run programs (like v4l2-ctl or setup-camera.sh) from Java with the Runtime class.

## Issue: image buffering (severe)

In 2016, we had an issue where the camera would return the same image multiple
times in a row (due to buffering by the camera), which becomes a problem as the
robot moves around.

### Solution:

Our solution (since 2016) was to retrieve 5 images from the camera and use the last one. Yeah, it's janky.
[Example from Rafael](https://github.com/Team694/Rafael/blob/master/src/com/stuypulse/frc2017/robot/cv/Cameras.java#L59-L63).

OpenCV allows you to set a buffer size property on cameras, but we weren't able to get [that](https://github.com/Team694/stuyvision-lib/blob/09bf768aae7e1b9ee49b5e2ade907bbc266c9e74/src/stuyvision/capture/DeviceCaptureSource.java#L32-L42) to work.

## Issue: big images are slow to process

We don't need (or want) high definition.

### Solution:

`stuyvision-lib` [resizes](https://github.com/Team694/stuyvision-lib/blob/22a3a576f7c4d776230681aba397520adcf5cb64/src/stuyvision/capture/CaptureSource.java)
images to a constant, small size. Also, `v4l2` can be used to reduce the
camera's resolution.

## Issue: mounting

Mounting the camera reliably has long been a problem. Plan ahead.

Check that it is pointed straight as part of systems check.
