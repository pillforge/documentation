VUMCR Platform Support
===========================

The Debugger Board uses the MSP430F5529 microcontroller. This is regarded as a third generation MSP430 microcontroller
and is represented as the x5xxx family in TinyOS. The TinyOS fork we started with only supports x1xxx microcontrollers.
However, work has been done on the tinyprod repo to support x2xxx and x5xxx families.

**Building**

We have developed a TinyOS platform for use with the Debugger Board.
The make target for this board is vumcr, thus the make command is.::

    $ make vumcr

**Flashing**

The proper Udev rules need to be set in Linux in order to have permission to use the USB programmers. Place the
following in /etc/udev/rules.d/82-msp430.rules and chmod it to 644.::

      #mspdebug
      SUBSYSTEMS=="usb", ATTRS{idVendor}=="0451", ATTRS{idProduct}=="f432", MODE="0666", GROUP="users"

      #msp430-bsl
      SUBSYSTEMS=="usb", ATTRS{idVendor}=="2047", ATTRS{idProduct}=="0200", MODE="0666", GROUP="users"

      #msp fet430uif
      SUBSYSTEMS=="usb", ATTRS{idVendor}=="0451", ATTRS{idProduct}=="f430", MODE="0666", GROUP="users"

      #Any Texas Instrument programmer
      SUBSYSTEM=="tty", ATTRS{manufacturer}=="Texas*",  MODE:="0666", GROUP="users"

      ### mspdebug


mspdebug can be used to program the MSP430 through the eZ430 emulation interface. The switches on the Debugger Board must be correctly configured (See Debugger Guide)
and the usb cable has to be connected. Additionally, mspdebug has to be installed on the host computer. On
ubuntu, assuming the correct repositories are set per the tinyos installation instructions, the command should be.::

    $ sudo apt-get install mspdebug

To install an app onto the Debugger Board, run.::

    $ make vumcr install mspdebug

Since mspdebug is used by default, the mspdebug part can be omitted. However, if there are multiple device connected and you want to program a specific one, the command above can be extended with the serial number (actually the first few unique numbers of the serial number) of the device to be programmed. A list of the serial numbers can be obtained by running.::

    $ mspdebug rf2500 --usb-list

Once the serial number is found (eg. 0612346), the command for programming it becomes.::

    $ make vumcr install mspdebug, 06

**mspdebug tilib**

The best way to use the MSP-FET430 jtag programmer is using the tilib library.
To install this library, find libmsp430.so and place it in /usr/lib32/ or /usr/lib
depending on whether it is 32 bit or 64 bit. Also make sure that mspdebug has the same
architecture (32/64 bit) as libmsp430. To install a 32 bit mspdebug in ubuntu, use::

     $ sudo apt-get install mspdebug:i386

The main problem with this approach is having to find libmsp430.so in the first place.
There are multiple ways to do this including compiling it from http://www.ti.com/tool/MSPDS or digging through Code Composer's installation files.

To flash/debug programs with this approach, run the following::

     $ make vumcr install tilib
or::

     $ mspdebug tilib
