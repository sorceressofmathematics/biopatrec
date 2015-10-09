# Communications #

All the routines associated with communications can be found in the **Comm** folder. These can be from/to peripherals or other software.

  * Analog Front-End (AFE)
    * Session-Based Interface (SBI)
    * other Custom Devices Interface
  * Virtual Reality Environment ([VRE](VRE.md))
  * Artificial Limb Controller ([ALC](ALC.md))

# Inputs #
## Analog Front-Ends ##
### Session-Based Interface ###

The SBI routines have been tested for the NI-USB6009, however, many other DAQ cards could be used under this paradigm, see ["About the Session-Based Interface"](http://www.mathworks.se/help/daq/about-the-session-based-interface.html). You can use the function [TestSBI\_NI\_USB6009](TestSBI_NI_USB6009.md) to test the different acquisition possibilities of SBI. In our experience, the NI-USB6009 is an affordable option for data acquisition.

The SBI can be used for both inputs and outputs, however, we mostly use it for inputs (recordings).

Since BioPatRec was developed before SBI, we also have available the "legacy" routines. See [Choose the Right Interface](http://www.mathworks.se/help/daq/choose-the-right-interface.html) for compatibility.

See [Troubleshooting](Troubleshooting.md) for issues.

### other Custom Devices Interface ###

In BioPatRec\_TRE, it has been added a new set of functions really useful in the case the user would like to use (or add) new custom acquisition devices. The use of new device will be totally transparent to the other BioPatRec functions like the recording session, feature extraction or pattern recognition and so on. To do this, the user must be able to write his own routines for the new device and properly place them in the correct files into the COMM/AFE folder.
Here few tips..

All the acquisition process must be divided into these .m files

![https://biopatrec.googlecode.com/svn/wiki/img/BioPatRec_TRE/BioPatRec_TRE_OCDfunctions.png](https://biopatrec.googlecode.com/svn/wiki/img/BioPatRec_TRE/BioPatRec_TRE_OCDfunctions.png)

#### ConnectDevice ####
This function creates and returns the connection object. Depending on how your peripheral communicates with the PC, you can use predefined Matlab functions to connect it, such as
  * obj = tcpip('localhost', 30000, 'NetworkRole', 'client') for Wireless connections
  * obj = serial('port','PropertyName',PropertyValue,...) for Serial connections

#### SetDeviceStartAcquisition ####
If your device needs some parameters passed by PC or every sort of setting procedure, all those routines should be here in this .m file. It must include all the setting parts to be done before the acquisition start. This function takes as parameter the connection object that has been made by the previous ConnectDevice function. In this way, it does not matter if your device communicates with wireless or serial protocol, as long as you use Matlab functions like fwrite(obj,'C','char'), the communication will work.
This function must also be able to send the start command to the device in way to begin the acquisition.

#### Acquire\_tWs ####
This functions returns a new window of samples. The number of acquired samples can be edited by the tWs (time window samples) parameter, it is passed in the function calling. So, here you can write your custom routines to get samples from your device.

#### StopAcquisition ####
This is used to send the stop acquisition command to the device.


### Biopotential Amplifiers ###

We have developed several low-cost, high-CMRR biopotential amplifiers for our research. We have specific designs for ENG and EMG. If you are looking for bio-amps, we might be able to help you.

## Other peripherals ##

  * AcceleGlove (coming soon...)

# Outputs #

We have established an easy communication protocol to produce physically meaningful outputs (see the Movements\_Protocol)

## Virtual Reality Environment ##

In order to easily test and quickly control a prosthesis from the BioPatRec, a Virtual Reality Environment ([VRE](VRE.md)) has been developed. Please see relevant page for more information.

## Prosthetic Devices ##

We have developed routines to control prosthetic devices using PWMs for servos or DC motors. The output command is transmitted using the Serial Communication Interface (SCI) to a microcontroller (see the Movements\_Protocol).