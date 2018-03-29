## Setting up Stuyvision-lib

The lib directory should have three things:

- jfxrt.jar
    - symbolic link to `/usr/lib/jvm/java-8-openjdk-amd64/jre/lib/ext/jfxrt.jar`
        - symbolic link to `../../../../../../share/java/openjfx/jre/lib/ext/jfxrt.jar`
- OpenCV-3.0.0.userlibraries
- opencv-341.jar
    - symbolic link to `/usr/local/share/OpenCV/java/opencv-341.jar`

The build.xml should also be updated with the version of opencv that you have downloaded

## Setting up cv-edu

The lib director should have 2 things:

- opencv-3.4.1
    - symbolic link to `/path/to/where/you/downloaded/OpenCV/`
- stuyvision.jar
    - should be the jar in `stuyvision-lib/dist/`

The Makefile and build.xml should be updated with the version of opencv that you have downloaded
