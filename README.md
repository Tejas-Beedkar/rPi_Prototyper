Raspberry Pi Prototyping Laptop
===============================
It's 2020... that is why this even exists :)
The aim was to create a rPi laptop that has a integrated GSM and a Arduino for rapid prototying of new ideas. I also adding in a breakout board to access the rPi GPIO port with ease. The aim is to create the following system 

![SysSch](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_System_Layout.jpeg)

Phase 1a
--------
Most of these systems need one of two things to survive regular use.

1. Effort - You design reliability into it by Failure mode and effects analysis

2. Time - You use it to failure and iterate it into success.

I am not going to spend the time into a FEMA when I can be building stuff. So option 2 it is. In Phase 1 I plan to stick the following components into place - 

* raspberry Pi
* raspberry Pi 5inch Display
* raspberry Pi breakout board
* Arduino Mega + Touch screen display
* The Targus ppk keyboard and keyboard adapter
* Power pack

The power budget is as follows - 

| Component                          | Power           |
| -------------------------------    | --------------- |
| raspberry Pi                       | 950 mA (5.0 W)  |
| raspberry Pi 5inch Display         | 460 mA  (2.6 W)  |
| Arduino Mega + Touch screen display| 200 mA  (1 W)    |
| The Targus ppk keyboard and keyboard adapter| 100mA   (0.5 W)|
| Total                              | 1710 mA (9.1W) |

That is way on the higher side. The power bank I chose was the [Mi 20000mAH Li-Polymer Power Bank 2i (Black) with 18W Fast Charging](http://www.amazon.com). It can give me 9V/2A output for a 18W power reserve, of which the current layout is eating 50%. Should have gotten the 30000mAh bank...

Moving right on - layout test. First thing to check is that everything can fit in the box. 

![LayoutVer1](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_LayoutVerfication1.jpg)

Note that I am fitting in stuff I don't plan to install now as well such as a joystick mouse and GSM module.

![LayoutVer2](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_LayoutVerfication2.jpg)

There seems to be space for eveything I need in the box. I omitted the USB cables since they are quite flexible and easy to get in small lengths. I am working on the assumption that they will fit into the final product.
Next we tune each component.

**Keyboard**

I had a old Targus Stowaway keyboard from the per dot-com bubble iPaq era. This keyboard does not have a USB port not a serial output - it uses a propritary port in true silicon vally fashion. Fortunatly [cy384](http://www.cy384.com/) has made a [fantastic set of instuctions](https://github.com/cy384/ppk_usb) to make you own adapter to overcome this customer lockdown feature. I version of the adapter is -

![KBAdapter](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_KB_Layout.jpg)

**Screen**

The screen I used was a 5 inch Kanman HDMI screen with touchscreen interface. The screen is old and has a crack that is messing up the touch screen calibration. I have left space in case I buy the 7 inch CSI interface screen in the future. For now, I am not implemention the touch screen port.

**Breakout Board Test**

The breakout board has a ribbon connector that is key-coded at the breakout board, but not at the rPi end. So we test the power pins to ensure that we have not connected it in reverse. That way we don't have a nasty surpirse once the assembly is completed.

![BreadBoardTest](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_BreakoutBoardTest.jpg)

Eating with chopsticks make you good at one handed multimeter probing :)

**Pre Assembly Test**
One thing I have learned when assembling HW in a rush and cooking pasta is that you test/taste at every step. So we power up the system in a pre-assembly test to make sure thing power up and there are no [unforseen consequences](https://www.youtube.com/watch?v=t8zmNU0AAJw) in the setup.

![PreAssemblyTest](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_PreAssemblyTest.jpgg)

So the screen did not get a HDMI signal. It had worked on a earlier test so I think it's a power issue in the rPi configurations. It will test that theory at a later stage. For now, I am proceeding with a acceptable on the Pre-Assembly Test.
Also ignore the readout on the Arduino. It's running a old pollution sensor program I had written - I did not clear it before the assembly.

**Assembly Test**

In phase 2, I am going to make custom 3D printed harnesses for each component. For now, a glue gun will do. I really love this because it gives me time to use the layout for a while before I say its got no convinience issues. And then I can peel off the glue and put in the permenant parts!

![Glue](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_Glue_Screens.jpg)

The aim is apply glue that you can access (its not between surfaces) and is not on sensitive parts so that peeling it off does not break anything.

![Phase1](https://github.com/Tejas-Beedkar/rPi_Prototyper/blob/master/images/re_Phase_1.jpg)

**Configuring the System**

The screen did not work on the first boot - it got no HDMI signal. Is suspect that this is because I had two adapters on the cable. The powerloss was corrupting the signal. You can increase the power by editing the /boot/config.txt file as follows:

	* hdmi_force_hotplug=1 makes sure the Pi believes the monitor/TV is really there.
	* config_hdmi_boost=4 or even higher (up to 9) if your display needs a stronger signal.
	* If the display is a computer monitor, use hdmi_group=1 and if it is an older TV, try hdmi_group=2.
	* Do not set hdmi_safe=1 as that overrides many of the previous options.

Also I had to rotate the screen as it was upside down - 

	* display_rotate=0 is the normal configuration
	* display_rotate=1 is 90 degrees
	* display_rotate=2 is 180 degress.
	* display_rotate=3 is 270 degrees

And Phase 1 is done!






