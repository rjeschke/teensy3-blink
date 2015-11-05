Blink for Teensy3 - Custom, simple Makefile starting point
---

#### Another Blink?
When I started with Teensy3 development myself, I quickly noticed that the Arduino sketch editor is maybe nice for small projects, but misses the power of a real IDE. As I am using Eclipse heavily for C and C++ development it was quite natural to be able to develop for Teensy3 using Eclipse. There are existing solutions out there, that give you makefiles, but I did not want to include the whole vanilla Teensy3 core for nothing or for small changes.

That's why I came up with this solution here. Basically you can just copy the `Makefile`, create a C/C++ file in the `src` folder and start developing. (Instructions on how to import the project into *Eclipse* are given below).


#### Supported platforms:
* Linux
* Possibly MacOS


#### Build instructions:

1. Download and install the [Arduino Software][1]
2. Download and install [Teensyduino][2]
3. Export an environment variable called `ARDUINO_HOME` that points to your *Arduino Software* installation
4. Connect your Teensy3.1+
5. Run `make upload`


#### Makefile targets
* `build`, `all` builds the `.hex` file without uploading
* `upload` builds and uploads to the Teensy
* `clean` cleans binary output
* `distclean` cleans everything
* `symbols` creates `$(OUT_PATH)/eclipse_cdt_symbols.xml` from definitions inside the `Makefile` for importing into Eclipse CDT


#### Makefile hacking
Feel free to mess around with the `Makefile`, most likely you will only need to modify the first few lines that contain the `M_*` variables.

* `M_PROJECT`: the project name and the name of the resulting `.hex` file
* `M_CPU_CLOCK`: your CPU clock in Hz
* `M_USB_TYPE`: the USB type
* `M_LAYOUT`: keyboard layout
* `M_ARDUINO_VERSION`: Arduino software version
* `M_TEENSYDUINO_VERSION`: Teensyduino version
* `M_CPU`: `__MK20DX256__` for Teensy3.1+, `__MK20DX128__` for Teensy3.0
* `M_OPTIMIZATIONS`: debugging and optimization switches


#### Overriding Teensy3 core files
You can create a folder called `teensy3` in your project's root for replacing/modifying Teensy3 core files. Just copy the file(s) you want to modify from your Teensy3 installation (`ARDUINO_HOME/hardware/teensy/avr/cores/teensy3`) into `teensy3` and start editing. The build process creates a folder called `teensy3.copy` that contains the vanilla core files and your modified ones.

This way you can have custom USB devices or similar changes on a per-project base without having to mess around with your *Teensyduino* installation.


#### Usage with Eclipse
1. Download/install [Eclipse][3] (if not already done)
2. You either need the *C++* edition or the CDT installed
3. File->New->C++ Project: Makefile Project->Empty Project, Toolchain: Linux GCC
4. Deselect *Use default location* and select this folder as the *Location*
5. Run `make symbols` on the command line
6. Project Properties->C/C++ General->Paths and Symbols, Import Settings...: look inside the `bin` folder for the XML


---
(c) 2015, René 'Neotec/Neet' Jeschke, [https://github.com/rjeschke/teensy3-blink][4]

[1]: https://www.arduino.cc/en/Main/Software
[2]: https://www.pjrc.com/teensy/td_download.html
[3]: https://eclipse.org/downloads/
[4]: https://github.com/rjeschke/teensy3-blink
