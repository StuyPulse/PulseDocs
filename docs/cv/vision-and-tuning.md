# Vision and Tuning

## `stuyvision-lib`
stuyvision-lib is a simple library with which you can run a GUI that makes it
easier to tune your vision code.

Overview of classes in `stuyvision-lib`:

- `abstract class CaptureSource`: an abstraction over ways of getting images. Subclasses:
    - `class DeviceCaptureSource`: basic wrapper around VideoCap (the OpenCV class representing a camera). This is
      the single part of stuyvision that uses OpenCV.
    - `class ImageCaptureSource`: gets an image from a file
    - `class VideoCaptureSource`: gets frames from a video file

- `VisionGUI` and `ModuleRunner`: These are the meat of it: `VisionGUI` puts
  all the sliders, tabs, images, etc. onto the screen and executes the vision
  code (each tab in the GUI runs in a separate thread). A `ModuleRunner` says
  *what* vision code to run and *on what* `CaptureSource` to run it.
  A `ModuleRunner` is a set of pairs of VisionModules (which have a
  `run(Mat frame)` method and some other stuff for the GUI) and `CaptureSource`s.
  For each pairing there is a tab in the GUI which repeatedly gets images from the
  `CaptureSource` and processes them with the VisionModule for that tab.

- `IntegerSliderVariable`, `DoubleSliderVariable`, `BooleanVariable`: during testing, the values
  stored in these objects are set by the sliders in the GUI. Thus, we can tune
  values in the vision code in the GUI. During production (i.e. when not
  running the GUI), they just have their default values, and are nothing
  special.

**Note:** There is some "magic" going on. `stuyvision-lib` uses reflection (a
feature of Java) to enumerate all of the fields in a VisionModule, pick out the
`IntegerSliderVariable`s, `BooleanVariable`s, etc., and create
sliders/checkboxes for them.

### VisionModule methods

These methods are available to all subclasses of `VisionModule`.

#### `void postImage(Mat frame, String label);`

Puts an image to the screen with a specified label. E.g.:

```java
postImage(frame, "Camera Frame");
```

#### `boolean hasGui();`

Returns whether your code is being run with a GUI. Useful for writing
code that posts images to a GUI when there is one, but still works
when there is no GUI.

```java
if (hasGui()) {
    postImage(frame, "Camera Frame");
}
```

#### `boolean postTag(String imageLabel, String tagKey, String tagValue);`

Adds a tag beneath the image labelled `imageLabel`.

`tagKey` is the label of the tag. If you call `postTag` multiple times with the
same `imageLabel` and `tagKey`, it replaces the old tag value with `tagValue`.

This is useful for displaying information about your frames. For example, if
you were calculating the distance to an object, you might want to show the
distance your code has calculated below the image.

```java
postTag("Filtered frame", "Number of contours", Integer.toString(numberOfContours));
```

## Useful OpenCV functions

In [cv-edu-2017](https://github.com/Team694/cv-edu-2017#opencv-functions)'s
README, there are descriptions of some often-used OpenCV functions.
