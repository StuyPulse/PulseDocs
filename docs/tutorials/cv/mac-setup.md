### Getting OpenCV on a Mac:
1. Get Homebrew from Terminal by typing ```/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"```
2. Get Ant by typing: ```brew install ant```
3. Run: ```brew edit opencv```
4. Find and replace the line ```DBUILD_opencv_java=OFF``` to ```DBUILD_opencv_java=ON```
5. Save the file and exit the text editor.
5. Run: ```brew install --build-from-source opencv``` to install OpenCV.
6. Wait a very very very long time.
- If it says the formula built, but isn't symlinked because the target already exists, force the link with: ```brew link --overwrite opencv```
- If it still doesn't work and says that OpenCV is not writable, run: ```sudo chown -R $USER /usr/local/share/OpenCV``` and try ```brew link --overwrite opencv``` again
7. Open your Finder and open the /usr/local/Cellar/opencv/3.4.1_5/share/OpenCV/java folder. There should be a .jar and .dylib file there.
8. If you didn't already, clone the cv edu repository. Then, open the Makefile and replace whatever OPENCV_JAR and OPENCV_LIBS are equal to to the correct paths to the .jar file for the JAR and the java folder for the LIBS.
8. Run ```make``` in the Terminal to make sure everything works. If it gives warnings that your compiler should be upgraded to major version 53, download Java 9, run ```/usr/libexec/java_home -V```, and then run ```export JAVA_HOME=`/usr/libexec/java_home -v <whatever is before the comma in the Java 9 line, ex: 9>```
9. Run ```make``` again and it should work without any warnings. 
