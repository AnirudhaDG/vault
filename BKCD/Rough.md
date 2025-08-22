Hi Georg,
Thanks for the reply. 
1. Device Choice:
	1. Due to a procurement issue on our side, we moved from the IQS9150 to the ISQ9151. Currently we are using the IQS9151 on our board.
	2. The design that we have sent to you is the design for a composite Keyboard/Mouse device. We call it keyboard but it has a trackpad too. A picture of the same has been attached herewith.
2. CT210A:
	1. We are using the IQS9151 GUI and IQS9151 Sample code as listed on your website: 
	   https://www.azoteq.com/design/software-and-tools/
	2. The Firmware for the CT210A could not be updated on our side due to an issue with the Azoteq Firmware Upgrader. The current version of out CT210A is v1.0.1. Upon entering DFU mode, the Firmware Upgrader dialogue box prompts us with a "No Azoteq devices found in DFU Mode". The screenshot of the same has been attached herewith.
3. Connections:
	1. Connections to the CT210 were made as per the AZD026 datasheet, as mentioned user section "Connecting USB-Dongle for Serial Communication". Section 3.3, I2C. The pinouts for the same have been attached herewith.
	2. We used the Arduino UNO and the connections were as follows:
		- SDA->SDA
		- SCL->SCL
		- RDY_Pin->D7
Do let us know if any further clarification is needed


Hi Georg,

The full tx-rx mapping is in the schematic attached above. To clarify your doubt, the trackpad IC has nothing to do with the Keyboard in itself. The architecture is as follows:
- There is a main MCU on board, the STM32G4 series, which is connected to the rows and colums of the keyboard matrix. 
- The i2c pins of the MCU are connected to the IQS9151.
- A detailed PDF of the entire schematic is attached hereforth. 
On the Arduino I did use a Logic Level Shifter to convert 5v signal to 3v3 signal. 
I will promptly update the firmware on my CT210A and get back to you on the same.