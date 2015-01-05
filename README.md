pixel_bots
==========

Ground Robot team for exploration and target acquisition.Fastest approach of three ground robots with to acquire weighted targets in a given maze to achieve the highest score in defined time interval.

==========
Pilot Phase<br>
To generate a path for a given map containing different shapes and autonomously navigate from start to end point using only Visual Feedback. The path to be generated is a tradeoff between total objects identified(including performing certain actions like glow LED's, Delay motion by 5s etc). The scoring is given by <br>
<br>
Total score = 20*P + (480-T)
* P=Shapes identified and performing actions attributed to the respective shape
* T=time taken for travel

Shape Properties:
- Black Square: Go forward
- Red Square : Go back
- White Square : Stop for 5s after the trailing edge of the bot crosses the previous shape.
- Blue Square: Glow  LED for 2s after the trailing edge of the bot crosses the previous shape.
- Plus sign: Four - way direction freedom
- Black Triangle : Turn Right or left depending on direction of the apex.
- Yellow Square: start point or Goal


More on the competition-http://www.techfest.org/pixelate and problem statement-http://www.techfest.org/resources/pixelate.pdf held from 2nd to 4th Jan 2015.

Basic Research:<br>
Learning basic motion planning algorithms like A* , D* , LPA* , D* Lite and deteriming the best one among them.<br>
References: 

* Planning Algorithms by S.Lavalle :http://planning.cs.uiuc.edu/book.pdf ,
* Sven Koenig's Homepage 
* RRT Homepage : http://msl.cs.uiuc.edu/rrt/about.html
* Wikipedia
* http://www.cs.cmu.edu/~motionplanning/lecture/AppH-astar-dstar.pdf

Hardware:<br>
Raspberry Pi, Wifi Adapter, Robot chassis with DC Motors, Power Bank, L298N motor Driver, Overhead webcam for Visual feedback.

======
Implementation: <br>
- Used OpenCV to detect all shapes. All shapes then fitted into a grid type matrix for grid based path planning algorithms
- Generated the best path which gets the highest score.Used a slight variant of A* motion planning algorithm. Here isntead of allocating costs in the heuristics we compare the properties of each cell whether its traversable or not.  
- Heading and position of Bot tracked using a triangular marker
- Communication with the onboard Raspberry Pi using Wifi by creating a local wifi hotspot. Sending characters for directional control using Network Socket.
- Visual feedback to correct course or give new commands (PID Implementation pending)

======
Code Description: There are total of 3 codes in this repository .

* src/main.cpp: Running on the PC . Overhead webcam to serve as video input.<br>
Algorithm:

  - Store the video capture as an image
  - Thresholding and shape detection to id. assigning row,column number from top left to bottom right. Getting (Y,X) of centre      of all shapes
  - generating a graph by adjusting all shapes into seperate rows and columns. Standard deviation value taken for adjustments
 

* src/serverc.cpp: Running on the PC 
Description

  - Send values after comparing to the server
  - Heading of robot calculated using  


* src/pixel_bots.py : Running on the PC<br> 
Description

  - Pins setup for motors and LED's 
  - Forward,Backward , Stop,Left ,Right control
  - receive character inputs for each control and call the respective function by comparing


=====
Youtube Video: 
Coming Soon!
