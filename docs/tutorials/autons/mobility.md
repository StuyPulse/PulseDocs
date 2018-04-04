#Mobility Auton

_Make your robot do something in Auton!_

Mobility auton is one of the most basic and fundamental aspects of the match. The robot moves autonomously to cross a line on the field, earning a small number of points for the match, and in some cases, being necessary for earning a qualification point. 

There are many ways to go about making mobility auton, ranging from very simple, to very complex. 

The simplest of which is setting a timer and letting the motors run until it runs out, when the robot is sure to have crossed the mobility line, and not run over to the other side, incurring a penalty. By using the built in timer in wpilib and setting it to a variable, and checking it in a loop, a team can have the motors run at any speed which allows them to cross the line. This can be mathematically figured out, or it can be simply tested with a straight drive forward test.

This can be slowly made more complicated, using various methods to check distance like line sensing, encoders, ramping, etc, but the former is a good basic way to get auton runnig very simply and with minimal testing.