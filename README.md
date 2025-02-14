## Documentation for fishertechnik Training Factory 4.0 9V 536629

### docs
**TXT-security**: Connecting to TXT controller via SSH, instructions for setting up ROOT password in order to gain root privileges\
**Update TXT**: Instructions to update firmware on the controllers\
**ROBOPro-manual**: Manual for using the ROBOPro software\
**536629-factory_simulation**: Introduction + breakdown of factory model\
**TXT Operating manual:** Manual for TXT 4.0 \
**ftrobopy-manual**: Manual for using the community tool ftrobopy, use python programming on the TXT controller

### links 
**fischertechnik's offical github:** https://github.com/fischertechnik \
**fishertechnik Community firmware:** https://github.com/ftCommunity/ftcommunity-TXT \
**Hubb Van Nuetrk's blo:** Lots of video tutorials with fischertechnik machines, https://niekerha.home.xs4all.nl/Robotics-Mirft2.html \
**fischertechnik forums:** Good for asking questions, community is quick to help. https://forum.ftcommunity.de/viewforum.php?f=8 (wil need to translate from german)

### papers 
https://perso.uclouvain.be/ramin.sadre/documents/txt_report_draft.pdf
https://arxiv.org/pdf/1910.00303

---
title: Fischertechnik 536629 Factory Simulation 9V Documentation
---

## Requirements
> All mentioned files can be found in [https://github.com/kbeeperez/ft-documentation/tree/main/docs](https://github.com/kbeeperez/ft-documentation/tree/main/docs)

Fischertechnik offers free software for interacting with their products downloadable at the link below. This factory simulation has 5 TXT 4.0 controllers that may require software updates, this can be done through ROBOPro 4.7.0. These applications can also be used to add or update programs that run each machine with ROBO Pro Coding or ROBOPro.

[https://www.fischertechnik.de/en/schools/apps-und-software](https://www.fischertechnik.de/en/schools/apps-und-software)

The ROBO Pro Coding App allows you to program models at different difficulty levels depending on the grade level. The application supports: Andriod, iOS, Linux, and Windows.


ROBOPro 4.7.0 is a Windows application, to run on a different OS requires a Windows virtual machine. This application allows you to create and test `.rpp` files, sample files for the training facility are available in the path: `Program Files (x86)\ROBOPro\Sample Programs\Training Models`, but all the necessary programs for the factory are in github [https://github.com/kbeeperez/ft-documentation/tree/main/ft-program](https://github.com/kbeeperez/ft-documentation/tree/main/ft-program)

## Backing up and updating controllers

If there TXT's become damaged, they can be fixed following: https://github.com/fischertechnik/FT-TXT/blob/master/TXT-Linux-FAQ.md#attach-serial-usb-converter

### TXT WEB server

Be sure to back up any programs or files on the TXT controller before updating, as it will overwrite everything on the controllers. 

The easiest way to download the files on the controller is to connect to the TXT web server through USB, though there are other ways of connecting such as Bluetooth or WLAN AP. TXT controller firmware version >= 4.5.0 contains an integrated WEB server that can be used. To check the firmware version of the TXT controller: `Settings -> info`. 

If the firmware version is **earlier** than 4.5.0 check if the files can be found in fischertechnik's github: [https://github.com/fischertechnik/txt_training_factory/tree/master/bin](https://github.com/fischertechnik/txt_training_factory/tree/master/bin)

To access the web server make sure that the WEB server is switched on, a "ws" symbol will be displayed on the TXT status bar.

![WEB server enabled](https://github.com/kbeeperez/ft-documentation/blob/main/imgs/settings.png)

The WEB page of the TXT controller can be accessed when the IP address is entered in the WEB browser (*Chrome or Firefox are recommended*) after the TXT has been connected via USB.

> USB: 192.168.7.2

The page is password protected.

> User: TXT

> Password: Four-digit number of the TXT controller displayed in the upper status bar on the TXT display (e.g. 6892 if "TXT-6892" is displayed)

![Password prompt]()

![TXT WEB server dashbaord](https://github.com/kbeeperez/ft-documentation/blob/main/imgs/web-dashbaord.png)

<p>

The TXT dashboard displays all the directories and files in the controller. The origanl programs can be downloaded in order to upload after the update.


A more detailed guide for acessing the TXT WEB sever can be found here: [https://github.com/fischertechnik/txt_training_factory/blob/master/doc/WEBServer.md](https://github.com/fischertechnik/txt_training_factory/blob/master/doc/WEBServer.md)

### 	Updating 
To have the most recent version, make sure the ROBOPro program is up to date by going to `Help -> Download Update`.

`Update TXT Controller Lernfabrik 40 9Ven.pdf` is a step by step guide on how to update the TXT controllers, 


## Programs
**ProcessingStation.rpp** has to run on the master controller (blue LED) of the multi processing station with oven \
**Sorting_Line.rpp** has to run on the controller of the sorting line \
**Warehouse_GripperRobot.rpp** has to run on the master controller (LED) of the high-bay warehouse 

The controller of the vacuum gripper robot is an extension of the warehouse and needs no extra program in order to work!

![ROBOPro example](https://github.com/kbeeperez/ft-documentation/blob/main/imgs/robopro-example.png)

## 536629 Factory Simulation

Working factory: https://www.youtube.com/watch?v=BApxuYlsT_w 

`536629-factory_simulation_9v_edu.pdf` is the manual for the simulation factory and covers the fucntion of all the parts. \
Ensure all TXT controllers are connected to power and on. \
The Highbay Warehouse (HBW) TXT is the Master controller and the Vaccum Gripper Robot (VGR) TXT is the extension. \
Program, Warehouse_GripperRobot.rpp, should be auto-loaded on the HBW TXT and ready to start, but if it is not, the file will be under the ROBOPro folder on the TXT. The HBW stored workpieces by color, the top level is White, second level is Red and last level Blue.


The Multi-Processing station with Oven (MPO) has a Master controller at the Milling and Ejector station while the Oven is controlled by the extension TXT. The program, ProcessingStation.rpp, should be loaded and ready to start. \

> notes: The WAN features on the MPO master TXT do not work properly, it does not connect to wifi. May need to be re-flashed.

Sorting Line and Color Detector (SL) are controlled by a single TXT program, Sorting_Line.rpp.

Start the workpieces in the Sorting Line, first row is White, second row is Red, and last row is Blue.
![Sorting Line](https://github.com/kbeeperez/ft-documentation/blob/main/imgs/Sortierstrecke-mit-Farberkennung%20(6).JPG)

The factory should run in a cycle as follows:
- The workpiece blocking the light sensor signal to the VGR that there is a piece ready to transport.
- The VGR picks up the work piece and delivers it to the conveyor belt at the HBW.
- The HBW will have pulled an empty storage container and bring it to the converyor built, the conveyor built will deliver the storage piece.
- Once the storage container reaches the end of the conveyor belt the VGR will release the workpiece and the conveyor built will return the storage container back to the HBW.
- The HBW will store the container, marking which shelves are occupied.
- After all workpieces have been stored the HBW will began moving them for processing.
- The VGR will deliver the workpieces to the MPO where they will go through a processing stage and then be delivered to the SL.
- The SL sorts workpieces by color and the cycle starts all over again.

If there is an issue and where the factories get stuck a gentle push or tap can help start the motor again. If the facotry is not running as descibed connect the TXT controller to a computer in order to do a interface test, the ROBOPro manual has examples on how to use it. 

This interface test allows you to check the light sensorss and motors are running correctly on each TXT controller, also allows checking while running program from ROBOPro terminal.

![ROBOPro Interface Test](https://github.com/kbeeperez/ft-documentation/blob/main/imgs/connections.png)



## Capturing traffic
Wireshark can be used to capture the traffic through USB connection to the TXT controller running the `WarehouseGripperRobot.rpp` on the ROBOPro terminal.

The TXT controllers can also be used at MQTT brokers, further intructions: https://github.com/fischertechnik/txt_training_factory/blob/master/TxtSmartFactoryLib/doc/MqttInterface.md /
The `ft-txt-bridge-cloud.conf` file is stored on the HBW controller under `/etc/mosquitto/` but root privliges are required to view/edit.

