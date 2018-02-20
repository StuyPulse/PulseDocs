#Problems with the JRE/JDK

As of 2018, Java Version 9 will not work with WPILIB. You must use Java 8.

Sometimes, the IDE will return an error when trying to deploy the code. The console will print something to the tune of the JRE being inadequate, or reference the its location. 

In order to fix this issue, you will have to go to go to:
    - Window > Preferences > Java > Installed JREs on Windows
    - Eclipse > Preferences > Java > Installed JREs on MacOS
    
Click on the JRE in the file chooser and edit it. Change the path to the JDK. Now try deploying your code, and voilá!