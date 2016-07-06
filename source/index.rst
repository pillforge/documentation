Welcome to Vanderbilt's MCR Developer's Guide!
=============================================
The goal of Vanderbilt's MCR project is to systematize
the development of miniaturized wireless
devices by creating a cyber-physical
design environment that will eliminate
barriers in the design process,
thus accelerating the progress
to prototyping.

This guide is for developers who wish
to use Vanderbilt's modular architecture
for their own project.

What you'll need
^^^^^^^^^^^^^^^^
- A SMAC debugger board
- An MCU module
- A wireless module and relay board (if communication with a base station is needed)
- Sensor and actuator modules as needed
- A SMAC flexible circuit
- An environment to write pure TinyOS applications, or Vanderbilt's WebGME environment

**Step 1:** Get an idea
-----------------------

Although the initial development for this project
was focused around medical devices, the platform
can be utilized for any project that necessitates
rapid prototyping of a small,
lightweight wireless system of sensors and actuators.

Connectivity between the sensor and actuator
modules is achieved with a flexible circuit*
on which the modules are mounted
before being folded to form the body of the MCR.

.. image:: flexible.jpg

The backbone can host up to five different modules
using 30-pin miniature connectors.
The developer must keep in mind that the center slot
is reserved for the MCU module*, and one slot is reserved
for the power management module. This leaves three
modules available for sensors and actuators.


**Step 2:** Choose modules
--------------------------

There are currently 9 existing sensing modules
and 3 existing actuation modules for the MCR:

.. image:: Module_chart.PNG


(in the future this will be an embedded chart with links
to pages that will have more information on each individual
sensor)

**Step 3:** Write code
----------------------

Just as the component-based approach on the hardware
side is beneficial, we have developed a design environment
utilizing TinyOS, which is a component-based operating
system for wireless sensor networks and embedded devices.
To program the MCU, you can either create your own application
with pure TinyOS representation, or utilize the graphical
design environment currently in development.

**Step 4:** Test and debug code
-------------------------------

To test, debug, and eventually implement the code,
there exists a debugger board* with all of the
functionalities of the flexible band, including
an identical MCU and the same wireless capabilities.
Refer to the :ref:`Debugger Guide <Debugger Guide>` for more information on
the board layout and functions.


**Step 5:** Install application on the flexible circuit
-------------------------------------------------------

When the modules have all been tested and debugged
on the debugger board, they must be attached to the
30-pin miniature connectors on the flex band. REMEMBER,
slot A is designated for the power module, slot C
is designated for the MCU, and the wireless module is docked
on top of the MCU. The band must then be plugged
into the debugger board and the application must be installed
to the MCU on the flexible band. The following shows the proper
way to attach the flexible band to the debugger board:

.. image:: Flex_to_Board.PNG

Once the application has been installed, the band can be folded
to fit into a smaller space.
To most efficiently compress the band,
follow the folding guide. NOTE: the largest gap between
modules is between slot B and C, and the smallest gap is
between C and D. This should help you with the initial
orientation of the band.

.. image:: Folding_guide.PNG

Links
^^^^^
.. _Debugger Guide:

.. toctree::
   :maxdepth: 2

   Debugger_Guide
   Module_Guide

Indices and tables
^^^^^^^^^^^^^^^^^^

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
