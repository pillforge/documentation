.. _VUMCR Platform Support:

VUMCR Platform Support
===========================

The Debugger Board uses the MSP430F5529 microcontroller. This is regarded as a third generation MSP430 microcontroller
and is represented as the x5xxx family in TinyOS.

**Building**

We have developed a TinyOS platform for use with the :ref:`Debugger Board <Debugger Guide>`.
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


mspdebug can be used to program the MSP430 through the eZ430 emulation interface. The switches on the Debugger Board must be correctly configured (See :ref:`Debugger Guide`)
and the usb cable has to be connected. Additionally, mspdebug has to be installed on the host computer.

**mspdebug tilib**

The best way to use the MSP-FET430 jtag programmer is using the tilib library.
To install this library, you must first find libmsp430.so and place it in /usr/lib32/ or /usr/lib
depending on whether it is 32 bit or 64 bit. To do this, download the MSP Debug Developer's Package
from http://www.ti.com/tool/MSPDS. You must create an account to access the download. Also make sure that mspdebug has the same
architecture (32/64 bit) as libmsp430. If the 64 bit version is needed, you must rename the file libmsp430_64.so to libmsp430.so within your /usr/lib directory.
To install a 32 bit mspdebug in ubuntu, use::

     $ sudo apt-get install mspdebug:i386

To flash/debug programs with this approach, run the following::

     $ make vumcr install tilib
or::

     $ mspdebug tilib
