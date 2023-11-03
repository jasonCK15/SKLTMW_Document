# Radar System Setup and the configuration.

## This article shows the basic setup and configuration for initializing the radar system.

### Hardware

In the whole system, it consists of different components, circuits and even the antenna. The system diagram is shown below:

### Hardware’s Introduction

![RadaSystemDiagram.drawio.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/RadaSystemDiagram.drawio.png)

1. HMC952
    
    2Watt Power Amplifier with Power Detector
    
2. HMC1056
    
    Mixer
    

1. ADF4159
    
    Frequency Synthesizer for Phased-Locked Loops
    
2. ADRF6520
    
    Programmable Low-Pass Filters and VGA
    

### Power Requirement

The system is powered by two RIGOL DP2000 Lab Bench Power Supplies. As the whole system required 5 power terminal to power up the whole system.

Note that it has a order to power up the terminal in the Power Supply, the following instruction will conduct the order and details about different power terminals. 

### First Power Supply:

 

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled.png)

Green Terminal: Phased Array Module 
(5.0V, 3.0A)

Red terminal: DAC (ADS41B29)
(5.0V, 3.0A)

### Second Power Supply:

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled%201.png)

Red Terminal: 
Monitor, MCU, DDS, ADRF6520, AF4159
(5.0V, 2.0A)

Yellow Terminal: 
Middle and Bottom Layers’ 952
(5.0V, 2.0A)

Blue Terminal: 
Top Layer’s 952
(5.0V, 2.0A)

### Powering up Order:

Red(M) → Yellow → Blue → Red → Green 

Reminder: The Red and Green terminal in the first power supply has no order of powering up. 

As the 952’s power will push to maximum rating if the MCU’s power is not yet powered, which causes burnt of the 952 IC. So it is important to power the MCU (Red Terminal with a M-sign), in order to avoid the damage of the 952 IC.

To determine the functionality of the 952 IC, it can do it by viewing the monitor display. If the monitor shows the clear word “ City University oof Hong Kong SKLTMW”, the monitor and the MCU works perfectly. The following picture shows the view of the correct display of the monitor.

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled%202.png)

If it displays incorrectly, please reset the MCU by pressing the reset button in the top hand side of the PCB Board (near the program flashing pin). The following picture shows the incorrect wording.

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled%203.png)

After powering it, it is good to power the 952 Module safely!

## Software

It is necessary to initialize some modules so that the system is able to be functional. 
After powering up the system, the ADRF6520 and ADF4159 requires initialization through official evaluation software.

In ADRF6520, 

![ADRF6520 GUI.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/ADRF6520_GUI.png)

In ADF4159, 

![ADF4159 GUI Connection Page.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/ADF4159_GUI_Connection_Page.png)

![ADF4159 GUI Configuration Page.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/ADF4159_GUI_Configuration_Page.png)

## Network

The FPGA data will transmit through the Ethernet. So it is necessary to setup the network environment to ensure the network’s operation. Lan Cables are connected to the Router, so the router will indicate the power blinking LED like the pictures show.

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled%204.png)

After connecting the Lan cable, user can access to the router’s control by typing the IP address: (192.168.1.1). It requires login password and name for accessing the interface. The following diagram shows the view of the login tab.

![Router Login Page.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Router_Login_Page.png)

Special Reminder: I have experienced the issue that cannot enter the interface, it found out that the browser disable the DHCP feature. By solving this, you can simply use the Window Diagnostic to solve the issue automatically.

- Username:  admin
- Password:   admin

The interface will be shown after finishing the login.

![Entering to the router.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Entering_to_the_router.png)

For searching the IP-address of the FPGA, simply typing the **URL: 192.168.1.1/DHCPTable.asp**

It will show the active IP Table and display all active device in the router’s LAN environment. Normally, the system is only consists of two devices: notebook and the FPGA, the notebook is usually have a host name. So that we can able to find out the FPGA’s IP-address, and the following picture shows the example of the DHCP IP Table.

![Checking the IP of the FPGA located.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Checking_the_IP_of_the_FPGA_located.png)

Reminder: This picture is just a example of the IP Table, IP-address may change if the connection is different or the router is being reset.

## GUI

The GUI is used for control the phased array module and receive the data from the FPGA, and plotting graph of the normalized data.

![GUI overview.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/GUI_overview.png)

To control modules, it uses the COM port to connect the module. For doing this, it requires setting the properties of the phased array modules.

### Property Setting

![GUI setting up the property of the antenna array.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/GUI_setting_up_the_property_of_the_antenna_array.png)

First, it required entering the size of the array. Simply typing the number of antenna in both x and y-axis separately. For reference, one module consists of 4*4 antenna.

Second, the spacing between antennas, and it is in ratio of wavelength λ . For reference, the module using is 0.612λ.

Third, choosing the Window function for the pulse creation.

Last but not least, it also provide the feature of beam configuration, which manually doing the beam steering, and different polarization of the antenna (LHP,RHP). Plot function is also provided.

### Connection to the Module

![GUI in the default connection page of the antenna array module.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/GUI_in_the_default_connection_page_of_the_antenna_array_module.png)

When doing the connection to the module, make sure the USB cable plug into the PC, and the module is ON. After that, pressing the “Find Port”, and then it will show the COM ports devices in the left hand side. The following picture shows the operation after pressing the “Find Port”.  Please be reminded that it will show all COM ports device connected to the notebook.

![GUI able to search the COM port.png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/GUI_able_to_search_the_COM_port.png)

By pressing the module, you can assign the module with the corresponding COM port name. The following picture shows the module in GUI are assigned successfully.

![GUI sucessfully connect to the module with the feedback .png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/GUI_sucessfully_connect_to_the_module_with_the_feedback_.png)

By validating the connection between the GUI and the module, user can try pressing the ON function and pressing the “Confirm” button. If the connection is valid, the data will feedback to the GUI. The following picture shows the feedback function.

![GUI sucessfully connect to the module with the feedback .png](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/GUI_sucessfully_connect_to_the_module_with_the_feedback_%201.png)

### Connection to the FPGA

In the display tab, Connection’s part is used for connecting to the FPGA through the LAN. IP address can be found the DHCP table in the router (See the Network Part). The following picture is used to show the connection part (not being connected to the FPGA).

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled%205.png)

After doing the connection correctly, the traffic light will change to Green Color.

### Conducting the Sweep Scan

By setting the mode, frequency step and the angle range. It can conduct the angle sweeping for the antenna array. Remember pressing the  disable button to change the status into able.

![Untitled](Radar%20System%20Setup%20and%20the%20configuration%20dcfe2c1b937948fc946d397c5a884202/Untitled%206.png)