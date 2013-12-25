433 RF Filter
=============

this is an rf receiver prefilter for the raspberry build with an attiny45. it prefilters the received signal to reduce the load for the raspberry that can i.e. run pilight (http://www.pilight.org).
you be warned: this could potentionally damage your raspberry pi and also other hardware. i take no responsability for anny damages! try at your own risk!

1. Install avrgcc:
------------------
	sudo apt-get install gcc-avr avr-libc

2. Install modified avrdude:
----------------------------
	wget http://project-downloads.drogon.net/files/avrdude_5.10-4_armhf.deb
	wget http://project-downloads.drogon.net/files/avrdude-doc_5.10-4_all.deb
	sudo dpkg -i avrdude_5.10-4_armhf.deb
	sudo dpkg -i avrdude-doc_5.10-4_all.deb
	
3. Compile and program attiny:
------------------------------
	make all
	
Additional info:
----------------
###Calculate fuses:
	http://www.engbedded.com/fusecalc/

###Pinout:

|  Name  | Raspberry Pi V2 | Attiny45 | 433 Receiver|
|--------|-----------------|----------|-------------|
|  MOSI  |       19        |    5     |      -      |
|  MISO  |       21        |    6     |      -      |
|  SCK   |       23        |    7     |      -      |
| RESET  |       24        |    1     |      -      |
| PI_IN  | see pilight cfg |    3     |      -      |
|REC_OUT |       -         |    2     |   DATA_OUT  |


to change the pins create an .avrduderc file in your home directory containing (the numbering is wiringpi numbering!):


	programmer
		id    = "gpio";
		desc  = "Use sysfs interface to bitbang GPIO lines";
		type  = gpio;
		reset = 8;
		sck   = 11;
		mosi  = 10;
		miso  = 9;
	;