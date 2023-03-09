*********************************************************************
SIM SCAN v2.00 (Mar 17 2003)
Copyright (c)1998-2003 Dejan Kaljevic
All Rights Reserved
(Web: http://users.net.yu/~dejan)
(eMail: dejan@net.yu)
*********************************************************************


DISTRIBUTION

You can freely make copies of the archive and distribute them as 
long as no alterations are made to the contents.


DISCLAIMER

THIS SOFTWARE AND ALL THE ACCOMPANYING FILES ARE PROVIDED "AS IS" AND 
WITHOUT ANY WARRANTIES EXPRESSED OR IMPLIED INCLUDING BUT NOT LIMITED TO 
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR 
PURPOSE. 

ANY MY LIABILITY WILL BE LIMITED EXCLUSIVELY TO PRODUCT REPLACEMENT. 
IN NO EVENT SHALL I BE LIABLE FOR ANY DAMAGES WHATSOEVER (INCLUDING WITHOUT 
LIMITATION, DAMAGES FOR LOSS OF BUSINESS PROFITS, BUSINESS INTERRUPTION,
LOSS OF BUSINESS INFORMATION, OR ANY OTHER PECUNIARY LOSS) ARISING OUT OF
THE USE OR INABILITY TO USE THIS PRODUCT.

All other trademarks mentioned herein are property of their respective
companies.


;******************************************************************************

			DESCRIPTION
			-----------


I MUST WARN YOU THAT YOUR CARD MAY BE DESTROYED DURING THE WORK WITH THIS 
PROGRAM !!!.


SIM SCAN is a program that allows functionality analysis of Yours GSM SIM
smart card.
Do not use this program on SOMEONE ELSE'S SIM CARDS, and you may use it only
in educational purposes!
Smart card reader needs no power supply, since it is powered via RS232 lines.

With this program you can analyze:

ATR 	(For any card)

CLA+INS (For any card, while comments are valid only for GSM SIM card)

FILES   (For any card, while comments and analysis are valid only for GSM SIM 
	card)

Ki	(It is valid only for GSM SIM MoU A3,A8 ciphering algorithm.)
	SOME CARDS CAN BE DESTROYED USING THIS FUNCTION!!!
	ESPECIALLY PREPAID CARDS!!! BECAUSE THEY HAVE LIMITED RUNNING
	OF A38 FROM 10000 TO 65536 TIMES AND AFTER THAT A38 DO NOT WORK ANYMORE!!!
	During the work it is possible to interrupt the program by pressing 
	any key. In case of interrupting, temp file will be saved, and later 
	you may continue the analysis from the point you've interrupted it.
	Also, at every 512 cipher texts temp file is automatically generated, 
	so that the analysis could be continued if a communication error with 
	card occurs.

Since almost all new SIM cards from 2000-2002 have limited running
of A38 to 65536, old method for finding Ki is useless.
I've found new method for finding Ki that can find Ki in range
from 3000 to 36000 cipher text.
Process takes at last 16 x less cipher texts than first
version of "Sim Scan"!

	New method can find 16 bytes Ki in next steps:

1) 2-R attack for getting first 2 bytes of Ki and take approx. 16000 cipher texts
2) 3-R attack for getting next 2 bytes of Ki and take approx. 758 cipher texts
3) 4-R attack for getting next 4 bytes of Ki and take approx. 758 cipher texts
4) 5-R attack for getting last 8 bytes of Ki and take approx. 832 cipher texts
	
That gives approx. 18348 cipher texts for finding Ki.

	This version of Sim Scan for non "Strong Ki" uses:

	1 x 2-R attack 16000
      + 1 x 3-R attack 758
      + 1 x 4-R attack 758
      + 1 x 5-R attack 1200
      + brute force on 4 bytes (2)
        ------------------------
      = approx. 18720 cipher texts.

For this method process takes on P2 1.5 Ghz and resonator of 10,24 Mhz
from 5 min to 45 min (approx. 20 min)!


	For "Strong Ki" Sim Scan uses approx. 65000 cipher text.


Note:	First time when you use option "Find Ki", program
	will create "par2.bin" and process will take on P2 715 Mhz
	approx. 1 hour.	


After finding Ki, IMSI and Ki will be stored in file and you can use
later to write IMSI and Ki to GSM a38 SIM based on Gold or Silver Wafer
cards (PIC 16F84 + 24lc16, 16F877 + 24lc64).
Source for Gold-Silver card can be found on my site: http://users.net.yu/~dejan

	Installation
	===========

Just run "install.bat". This will create DIR "c:\Sim_Scan" and copy 
appropriate files.

	Multi RUN of Sim Scan
	=====================
If you have 2 or more available COM ports and SIM card readers, you can
scan 2 or more card in same time. But first you have to make different
DIRs for each copy of "Sim_scan.exe" and to RUN exactly from 
those DIRs.

	Example:  For Starting 3 "Sim Scan" in same time.

	make DIR c:\sim_scan1 and copy "Sim_scan.exe"
	make DIR c:\sim_scan2 and copy "Sim_scan.exe"
	make DIR c:\sim_scan3 and copy "Sim_scan.exe"	

	Connect three SIM Card readers to appropriate COM ports.
	(COM1, COM2, COM3, etc.)
	Insert three SIM Card to appropriate SIM Card readers.

	Go to DIR c:\sim_scan1 and RUN "Sim_scan.exe".
	(You can select COM1 and to start finding a Ki from SIM card 1)
	
	Go to DIR c:\sim_scan2 and RUN "Sim_scan.exe"
	(You can select COM2 and to start finding a Ki from SIM card 2)

	Go to DIR c:\sim_scan3 and RUN "Sim_scan.exe"
	(You can select COM3 and to start finding a Ki from SIM card 3)

	
Note:
	You can also use USB to COM port interface, but be sure if
	your USB to COM port supports non standard baud rates.


	Strong Ki mode
	==============

If you are not sure that your SIM uses "Strong Ki", try first to 
find Ki in normal mode. If first pair of Ki are not found after 
60000 cipher text, press "cancel" to exit process, select "Strong Ki" mode 
and run it again!. If that gives no result then your SIM card is NOT
COMP128v1.



REQUIREMENTS:

- Pentium II processor with 64MB RAM
- Win9x


;----------------------------------------------------------

Update:

v2.00	
	This is win32 application made in 100% assembler!
	Improved 3-R and 4-R algorithm for finding Ki from SIM with COMP128v1.
	Added 5-R attack and "Strong Ki" attack.
	Fixed lot's of bugs.

v1.33
	Improved algorithm for getting Ki from SIM MoU a38 cards.	
	(Added 4-R attack).

v1.21
	Added function F6 for writing IMSI and Ki to GSM SIM Gold Wafer
	(PIC 16F84 + 24lc16).
	Improved algorithm for getting Ki from SIM MoU a38 cards
	(Added 3-R attack).

v1.10
	Fixed some bugs.

	Using Setup you can to set COM port and COM port speed.

	If you want to change COM port speed (that will speed up 
	ALL SimScan function!) you'll need to use appropriate resonator
	in Smart Card Reader!
	You can use resonator of 10.240 Mhz from old cordless phone
	and it will speed up about 2.5 x to 3 x using COM port speed 28800.
	It seems that all SIM card works fine on that speed!

	Also, this version support entering PIN 1.


*********************************************************************
Program is tested on Win95,98 and on Intel cpu's P1, Celeron.
If you have any problem with this program then just DO NOT USE IT!!!
*********************************************************************


Dejan Kaljevic