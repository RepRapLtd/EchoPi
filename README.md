# EchoPi

This is a device that uses the Raspberry Pi Zero as a WeMo device to turn on mains-powered items in your home using the Amazon Echo/Echo-Dot and their Alexa voice-recognition system.

## Safety

This uses mains electricity.  Mains will kill you if you touch it.  So don't.

The maximum current that this can switch is 1 amp.  With 220-volt mains that means a maximum 200W load; with 110-volt mains that means a maximum 100 W load.  The device is designed with a fuse holder.  Fit this with a 1 A fuse.

Parents: we set no age limits here - there are twelve-year-olds who could have organised D-Day, and there are thirty-seven-year-olds who can't be trusted with a penknife.  But don't let your children experiment with this unless you are confident that they are responsible and sensible.

Realistically, you will probably want to operate this with the cover off when you are setting it up.  Plug everything in to a disconnected extension cable and connect everything up.  Then - without touching anything to do with the uncovered case - plug the extension into a wall socket and turn it on.  Turn off and unplug the wall socket before you touch anything again.

## Electronics

The Eagle (https://cadsoft.io/) circuit design is single sided with a few jumpers.  It is intended to be produced by milling, though you can etch it conventionally as well of course.

The device incorporates a mains USB charger (red in the picture below).  This both acts as the plug so the device can be plugged into a wall socket, and as a 5V supply for the Raspberry Pi Zero and the rest of the electronics.

You will have to hack the charger attaching wires to the three mains connections inside and drilling holes to lead them out of.  The neutral and earth run straight through the device to the mains output, and the live wire goes through the fuse and then the opto-isolated phototriac, which switches it on and off. 

## Mechanics

![alt tag](blob/master/Pictures/case-cad.png)

The FreeCAD (http://www.freecadweb.org/) case is designed to be 3D printed.  

## Software Quick Start

1. Create a [Python Virtual Environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/),
2. git clone *this_repo*
3. cd *this_repo*/Software
4. pip install -r requirements.txt
4. nohup python lights.py > /dev/null &
6. Tell Alexa, "Alexa, discover my devices."
7. Say, "Alexa, turn off lights," and, "Alexa lights on," to switch the mains socket off and on.

The line in the Python lights.py program that sets the Alexa name of the device is this one:

     TRIGGERS = {"lights": 52000}

Change the "lights" to any name you like, but it's best to choose easily-pronouncable dictionary words or well-known propper nouns.  That way the Alexa speech recognition will be most reliable.

This is intended to connect to your home network using WiFi, but (particularly with BT HomeHubs) getting your Echo/Echo-Dot to find the device can be tricky.  

Start by turning off all the annoying "features" of the BT hub: disable Smart Setup; don't synchronise 5 GHz WiFi with 2.4 GHz (keep the passwords the same, though, or you'll never remember, and ignore the password warning it gives you when you do this); turn off Extended UPnP security.

Then use a micro-USB-to-ether adapter to connect the Pi Zero by wire to your hub.  Find the IP address that the hub has allocated your device (hub advanced settings; DHCP table).  Log into the Pi using ssh and set it to use that IP address for both wired and WiFi connections (https://www.modmypi.com/blog/how-to-give-your-raspberry-pi-a-static-ip-address-update).

Run the Python program and tell Alexa to discover your devices.  She should find it.  Test that it works by turning the load on and off.

Then shut everything down and disconnect it.  Fit a micro-USB-WiFi adapter in place of the ethernet and power everything up again.  You should be able to ssh into the Pi as before.

Ask Alexa to turn your device on.  If she sees it, great.  But if not, press and hold the Echo/Echo-dot button to put it into setup mode and leave it for a minute or so, then press and hold it again to turn setup off.  It should reconnect to your hub and then be able to turn your device on and off.


## Useful Links

Turn a Pi into an Echo/Echo-Dot equivalent:

http://www.instructables.com/id/Hacking-the-Amazon-Echo/

WeMo - the protocol used:

https://www.wemo.com/

## Acknowledgements

This is an extended fork of Todd Medema's repository here:

https://github.com/toddmedema/echo

Many thanks to him.

## Licence

GPL

