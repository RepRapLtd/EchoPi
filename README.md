# EchoPi

![FreeCAD design](https://raw.githubusercontent.com/RepRapLtd/EchoPi/master/Pictures/case-cad.png)

This is a device that uses the Raspberry Pi Zero as a WeMo device to turn on mains-powered items in your home using the Amazon Echo/Echo-Dot and their Alexa voice-recognition system.

## Safety

This uses mains electricity.  Mains will kill you if you touch it.  So don't.

The maximum current that this can switch is 1 amp.  With 220-volt mains that means a maximum 200W load; with 110-volt mains that means a maximum 100 W load.  The device is designed with a fuse holder.  Fit this with a 1 A fuse.

Parents: we set no age limits here - there are twelve-year-olds who could have organised D-Day, and there are thirty-seven-year-olds who can't be trusted with a penknife.  But don't let your children experiment with this unless you are confident that they are responsible and sensible.

Realistically, you will probably want to operate this with the cover off when you are setting it up.  Plug everything in to a disconnected extension cable and connect everything up.  Then - without touching anything to do with the uncovered case - plug the extension into a wall socket and turn it on.  Turn off and unplug the wall socket before you touch anything again.

## Electronics

The Eagle (https://cadsoft.io/) circuit design is single sided with a few jumpers.  It is intended to be produced by milling, though you can etch it conventionally as well of course.

The device incorporates a mains USB charger (like this: https://www.amazon.co.uk/Quality-Charger-Blackberry-Love-Accessories/dp/B01M2XE8V9/ ; red in the picture above).  This both acts as the plug so the device can be plugged into a wall socket, and as a 5V supply for the Raspberry Pi Zero and the rest of the electronics.

You will have to hack the charger by attaching wires to the three mains connections inside and drilling holes to run them out of.  The neutral and earth run straight through the device to the mains output, and the live wire goes through the fuse and then the opto-isolated phototriac, which switches it on and off.   

## Mechanics

The FreeCAD (http://www.freecadweb.org/) case is designed to be 3D printed.  

## Software

See here to create a linux image on an SD card for the Pi Zero:

https://www.raspberrypi.org/documentation/installation/installing-images/linux.md

Boot up the Pi Zero.  Change it's name to something you want:

http://www.howtogeek.com/167195/how-to-change-your-raspberry-pi-or-other-linux-devices-hostname/

Set your timezone:

http://www.geeklee.co.uk/update-time-zone-on-raspberry-pi-with-raspbian/

Set your Pi to have a static IP address, giving it the same one for ethernet and WiFi (you're not going to use both at once):

https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update

Setup your WiFi network and password:

https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/setting-up-wifi-with-occidentalis

Next get and run the EchoPi software:

$ git clone https://github.com/RepRapLtd/EchoPi.git

$ cd EchoPi/Software

$ pip install -r requirements.txt

$ nohup python echopi.py > /dev/null &

Tell Alexa, "Alexa, discover my devices."

Say, "Alexa, turn off device," and, "Alexa device on," to switch the mains socket off and on.

The line in the Python echopi.py program that sets the Alexa name of the device is this one:

     TRIGGERS = {"device": 52000}

Change the "device" to any name you like, but it's best to choose easily-pronounceable dictionary words or well-known proper nouns.  That way the Alexa speech recognition will be most reliable.

This is intended to connect to your home network using WiFi, but (particularly with BT HomeHubs) getting your Echo/Echo-Dot to find the device can be tricky.  

Start by turning off all the annoying "features" of the BT hub: disable Smart Setup; don't synchronise 5 GHz WiFi with 2.4 GHz (keep the passwords the same, though, or you'll never remember, and ignore the password warning it gives you when you do this); turn off Extended UPnP security.

Then use a micro-USB-to-ether adapter to connect the Pi Zero by wire to your hub.  

Run the Python program and tell Alexa to discover your devices.  She should find "device" (or whatever you have called it).  Test that it works by turning the load on and off.

Then shut everything down and disconnect it.  Fit a micro-USB-WiFi adapter in place of the Ethernet and power everything up again.  You should be able to ssh into the Pi as before.

Ask Alexa to turn your device on.  If she sees it, great.  But if not, press and hold the Echo/Echo-dot button to put it into set-up mode and leave it for a minute or so, then press and hold it again to turn set-up off.  It should reconnect to your hub and then be able to turn your device on and off.

The "nohup python echopi.py > /dev/null &" command will run the Python program in the background and it will stay running until you re-boot the Pi.  If you want to see what it is doing, just run "python echopi.py" instead.  But this will die when you log out.

If the program is running in the background and you want to kill it and start again, type:

$ ps -ael | grep pyth

This will give something like:

  0 S  1000   868   834 41  80   0 -  4062 poll_s pts/0    00:00:02 python

The number of the Python process is the 868.  To stop process 868 type:

$ kill -9 868


## Useful Links

Turn a Pi into an Echo/Echo-Dot equivalent:

http://www.instructables.com/id/Hacking-the-Amazon-Echo/

WeMo - the protocol used:

https://www.wemo.com/

## Acknowledgements

This is an extended fork of Todd Medema's repository here:

https://github.com/toddmedema/echo

Many thanks to him.

It uses the Raspberry Pi Zero Eagle Library from here:

https://www.raspberrypi.org/forums/viewtopic.php?f=63&t=127228

So thanks to them too.

## Licence

GPL

