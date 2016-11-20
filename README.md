# EchoPi

This is a device that uses the Raspberry Pi Zero as a WeMo device to turn on mains-powered items in your home using the Amazon Echo/Echo-Dot and their Alexa voice-recognition system.

## Safety

This uses mains electricity.  Mains will kill you if you touch it.  So don't.

The maximum current that this can switch is 1 amp.  With 220-volt mains that means a maximum 200W load; with 110-volt mains that means a maximum 100 W load.  The device is designed with a fuse holder.  Fit this with a 1 A fuse.

Parents: we set no age limits here - there are twelve-year-olds who could have organised D-Day, and there are thirty-seven-year-olds who can't be trusted with a penknife.  But don't let your children experiment with this unless you are confident that they are responsible and sensible.

Realistically, you will probably want to operate this with the cover off when you are setting it up.  Plug everything in to a disconnected extension cable and connect everything up.  Then - without touching anything to do with the uncovered case - plug the extension into a wall socket and turn it on.  Turn off and unplug the wall socket before you touch anything again.

## Electronics

The Eagle (https://cadsoft.io/) circuit design is single sided with a few jumpers.  It is intended to be produced by milling, though you can etch it conventionally as well of course.

## Mechanics

The FreeCAD (http://www.freecadweb.org/) case is designed to be 3D printed.  It incorporates a mains USB charger.  This both acts as the plug so the device can be plugged into a wall socket, and as a 5V supply for the Raspberry Pi Zero and the rest of the electronics.

You will have to hack the charger attaching wires to the three mains connections.  The Neutral and Earth run straight through the device to the mains output, and the live wire goes through the fuse and then the opto-isolated phototriac, which switches it on and off. 

## Software Quick Start

1. Create a [Python Virtual Environment](http://docs.python-guide.org/en/latest/dev/virtualenvs/)
2. git clone *this_repo*
3. cd *this_repo*/Software
4. pip install -r requirements.txt
4. nohup python lights.py > /dev/null &
6. Tell Echo, "discover my devices"
7. Use Echo's "turn off lights" and "lights on" to switch the mains socket on and off

The line in the Python lights.py program that sets the name of the device is this one:

     TRIGGERS = {"lights": 52000}

Change the "lights" to any name you like, but it's best to choose easily-pronouncable dictionary words or well-known propper nouns.  That way the Alexa speech recognition will be most reliable.

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

