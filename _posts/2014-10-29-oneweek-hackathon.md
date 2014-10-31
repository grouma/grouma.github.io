---
layout: post
title: //Oneweek Hackathon
comments: true
---

A couple months ago I competed in //Oneweek, the first-ever Microsoft company wide Hackathon. The week was kicked off by a company forum where leadership set priorities for the year, followed by two-days of pizza and coffee filled hacking. The fun ended in a two day Product Fair where all hacks were shared and voted upon. I was fortunate enough to work on the Eye Gaze Wheelchair hack which not only won the Tech for Good award, but also won the overall Hackathon.

<center>
![Oneweek Award](/public/images/oneweek-award.jpg)
</center>

### The Hack

Creating a hack team was facilitated with the use of an internal website. Users could pose hack ideas or browse and join existing teams. I was actually quite impressed with the website and it definitely promoted cross core collaboration. In fact, the team I worked with had all the cores of Microsoft represented. When I read the idea of the Eye Gaze Wheelchair hack I immediately knew I had to help out. The idea, although ambitious, was quite simple, enable a user to drive a wheel chair with only the use of their eyes. If successful, I knew it would be extremely rewarding, as well as a great opportunity to learn more about hardware.

The hack consisted of four parts, Tobii eye gaze tracking for Windows, an eye gaze "Joystick" application, Kinect-based "Safe Drive" for obstacle avoidance, and a microcontroller interface to a power wheelchair. The Tobii device was connected to a Surface Pro 3 running the eye gaze joystick application while the Microsoft Robotics Runtime was running on a second Surface Pro 2 connected to the Wheelchair and a Kinect camera. Below I will briefly discuss the implementation of the hack.

### Tobii Eye Gaze for Windows

Eye gaze information was provided to the eye gaze applications using an existing “Eye Tracker Host” application from MSR. This application interfaced with the Tobii hardware and then published the gaze position using a windows socket. This completely abstracted the job of eye-tracking away from the application. More information on the Tobii hardware can be found on their <a href="http://www.tobii.com">website</a>.

### Eye Gaze "Joystick" Application

The joystick application was created during the hackathon and displayed a live view from the forward-facing Kinect camera on the remote wheelchair and allowed the user to direct it to turn in place left or right, move forward, or stop by gazing at locations on the screen.

<center>
!["Joystick" Application](/public/images/joystick-application.jpg)
</center>

The location of the user’s gaze was displayed as a red dot on the screen. The application “smoothed” the output from the eye-gaze tracker using a simple averaging filter to produce a more stable point of gaze.

To prevent un-intended wheelchair motion, each region also had a “heat-up” time wherein the area would be gradually de-dimmed until the gaze had persisted there for some small amount of time. The system was “off” or “stopped” until the user gazed at the Start region for several seconds. Then the system became active and would publish drive commands to be used by the robotics “Safe Drive” system to move the chair. 

To stop, the user would direct their gaze away from the surface entirely, or at the “stop” region. When the “stop” region was activated after several seconds of persistent gaze, the system became inactive until the “start” region was activated again. The Joystick application communicated with the lower-level robotic control via a WCF protocol and connection created during the hackathon.

### Kinect-based "Safe Drive" for Obstacle Avoidance

The Microsoft Robotics team’s existing Kinect-based Autonomous Navigation solution includes dynamic obstacle detection and avoidance that takes “suggested” direction input and fuses it with Kinect and other sensor data to produce a “safe” trajectory. For the hack, the MSR Robotics Runtime processed the Kinect sensor data in real-time to detect the floor and identify potential obstacles and calculate an appropriate speed and heading for the wheelchair based on the eye gaze application’s input.   

<center>
![Safe Drive](/public/images/safe-drive.jpg)
</center>

During the hack, the existing “suggestion drive” component was enhanced to include a WCF interface to receive suggested trajectory information from the eye gaze wheelchair control app and to publish the camera images coming from the Kinect.

### Microcontroller Interface to Wheelchair

This is the portion that I worked on so I will be able to provide a little more detail. 

Once a safe trajectory is calculated it needs to be communicated to the chair. A lengthy web search on the model of the wheelchair revealed that the control interface used a proprietary CAN-bus communication. Although the manufacturer (Permobil) of the chair eventually shared the protocol, we determined that reworking this interface was infeasible in time for the hack. Instead we opted to replace the mechanical joystick with an Arduino. (I want to personally thank Permobil for their amazing contribution with this project and their continued support)

Internally, the joystick contains an 8-pin ribbon cable that connects to the chair controller board. Thankfully, <a href="http://forum.arduino.cc/index.php/topic,158256.0.html">someone</a> had already done the hard work and determined the voltages across the wires for each of the positions of the joystick. Essentially, when the joystick is moved completely in a single direction, i.e. forward, backward, left or right, a pair of pins will either go low (1.1V) or high (3.8V) while the remaining pins stayed at 2.5V. If the joystick was moved partially in a single direction, then the voltage across a pair of pins will be in between the above values. Moving the direction of the joystick in multiple directions at once e.g. towards 10 o'clock, resulted in voltages across multiple pairs of pins fluctuating in correspondence to the joystick's x and y component.

After discovering this information I immediately replaced the joystick and connected the ribbon to the Arduino's PWM ports. It is important to note that the wheelchair expects all pins to be at 2.5V upon bootup. Unfortunately, I kept receiving mysterious joystick connection errors when turning on the wheelchair. After a lot of head scratching, and busting out a variable power supply, it was determined that the wheelchair control board did not like the PWM signals and instead required a steady voltage. To circumvent this issues, each PWM signal was processed through a simple solid-state <a href="http://en.wikipedia.org/wiki/Low-pass_filter">low-pass filter</a> to produce the necessary steady-state voltages. The first time I actually got the device working can be seen <a href="http://instagram.com/p/rEdv4Gkzdb">here</a>.

I abstracted the Arduino through a simple C# library which exposed an interface to send a movement vector. The library contained a basic handshake protocol to connect the Surface device to the Arduino over a serial port. The library would then translate a movement vector into corresponding voltages and send them to the Arduino through a custom communication protocol.

One interesting thing to note, is a problem which occurred during testing.  The voltage output from the PWM ports varied depending on if the Arduino was connected directly to the surface or through a USB hub. This caused issues when turning the wheelchair on since the resting level across the 8-pin ribbons strayed too far from 2.5V. To remedy this issue, the C# library had a configurable "middle" voltage value.

### Result

Quite miraculously, the first person to ever use the completed device was former football star Steve Gleason. He has been living with amyotrophic lateral sclerosis (ALS) which I'm sure you are all too familiar with thanks to the Ice Bucket Challenge. Steve was the initial inspiration for the project. He traveled from New Orleans, where he lives, to the Microsoft campus specifically to work with our hack team. I have never been more satisfied and proud then standing over Steve's shoulder and watching the wheelchair spring to life with the movement of his gaze. Check it out in action below.

<center>
<iframe width="560" height="315" src="//www.youtube.com/embed/uAtErSwfmAc" frameborder="0" allowfullscreen></iframe>
</center>



