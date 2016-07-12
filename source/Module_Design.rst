Module Design Guide
===================

If other sensors or actuators are needed to accomplish
your specific project,
it is possible to develop them independently.
The following shows important pin locations on the
30-pin minature connector attached to the fleible circuit,
where the module would be mounted:

-	Pins 1 and 16 are for the voltage supply
-	Pins 2, 17, and 31-34 are ground
-	For SPI mode

	- Pin 4 is the chip select
	- Pin 11 is MISO
  -	Pin 12 is MOSI
  -	Pin 13 is CLK

-	For I2C mode

  - Pin 9 is Data
  -	Pin 10 is Clock
