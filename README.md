## Documentation for fishertechnik Training Factory 4.0 9V 536629

Working factory: https://www.youtube.com/watch?v=BApxuYlsT_w \

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

### TXT WEB server

Be sure to back up any programs or files on the TXT controller before updating, as it will overwrite everything on the controllers. 

The easiest way to download the files on the controller is to connect to the TXT web server through USB, though there are other ways of connecting such as Bluetooth or WLAN AP. TXT controller firmware version >= 4.5.0 contains an integrated WEB server that can be used. To check the firmware version of the TXT controller: `Settings -> info`. 

If the firmware version is **earlier** than 4.5.0 check if the files can be found in fischertechnik's github: [https://github.com/fischertechnik/txt_training_factory/tree/master/bin](https://github.com/fischertechnik/txt_training_factory/tree/master/bin)

To access the web server make sure that the WEB server is switched on, a "ws" symbol will be displayed on the TXT status bar.

![WEB server enabled](/home/kat/Desktop/ft-factory-simulation/pictures/Screenshot%202024-07-02%20at%2011.45.15%E2%80%AFAM.png)

The WEB page of the TXT controller can be accessed when the IP address is entered in the WEB browser (*Chrome or Firefox are recommended*) after the TXT has been connected via USB.

> USB: 192.168.7.2

The page is password protected.

> User: TXT

> Password: Four-digit number of the TXT controller displayed in the upper status bar on the TXT display (e.g. 6892 if "TXT-6892" is displayed)

![Password prompt](/home/kat/Desktop/ft-factory-simulation/pictures/Screenshot%202024-07-02%20at%2012.54.25%E2%80%AFPM.png)

![TXT WEB server dashbaord](/home/kat/Desktop/ft-factory-simulation/pictures/Screenshot%202024-07-02%20at%2012.59.03%E2%80%AFPM.png)

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

## 536629 Factory Simulation

`536629-factory_simulation_9v_edu.pdf` is the manual for the simulation factory and covers all the parts.

## Capturing traffic
Wireshark can be used to capture the traffic through USB connection to the TXT controller running the `WarehouseGripperRobot.rpp` on the ROBOPro terminal.

