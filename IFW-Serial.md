# IFW Serial Commands

The IFW Filter Wheels use a serial protocol for communication. The port should be set to 19.2 K baud rate with 8 data bits, 1 stop bit, and no parity (8N1). Responses are terminated with a LF/CR. See the Python Example (<https://github.com/OptecInc/fw-python>) for a sample communication program.

## Commands

### WSMODE

Return: !

Function: This command initializes the serial connection the PC and the IFW.
WSMODE causes the IFW program to enter into the main serial loop which checks
for additional inputs along the RJ-12 connector. A successful return from this
command is required before the IFW will accept any other user commands,

Warning: If not returned repeat WSMODE. There is a possibility that the command will timeout. This is also true if the wheel is being operated manually when the
WSMODE is sent.

### WHOMES

Return: single character A - K, which is the Wheel ID

Function: Make wheel find position 1 and identify filter wheel . Load from EEPROM set offilter names that relate to filter wheel.

Warning:

It may take up to 20 seconds for HOME function to complete.

ER= 1 is returned if number of steps to find position I is excessive.

ER= 3 is returned if filter ID is not found successfully.

### WIDENT

Return: single character A - K, which is the Wheel ID

Function: This returns the identity (Wheel ID) of the filter wheel to the PC.

### WFILTR

Return: 1 - 8

Function: This returns the current filter position.

### WGOTOx

x = 1, 2, 3, 4 or 5 (6, 7 or 8 for 8-position wheel)

Return: *

Function: Wheel will go to selected filter position “x”. No further command should be sent until the “*” character is returned.

Warning:

ER=4 is returned if the wheel is stuck in a position

ER=5 is returned if a number not in the set (1, 2, 3, 4, 5) is sent or (1,2,3,4,5,6,7,8) for 8-position wheels

ER=6 if the wheel is slipping and takes too many steps to the next position

### WREADS

Return: A string with the filter names

Function: This command returns a string of 40 characters (64 characters for 8-position wheels) that are the stored names for the filters in the current wheel. Each filter name consists of 8 characters.

### WLOADy*n

y = Wheel ID (A - K)

n is exactly 40 or 64 characters (plus termination), depending on the number of filters. Each filter has exactly 8 characters, unused may be ascii 0.

Return: !

Function: This command allows the user to program the on board EEPROM with the filter names for a selected filter wheel. After sending the string, you must wait a minimum of 10 ms before entering another command to allow time for the microcontroller to program the on board EEPROM. If data is received and stored successfully, a “ DATA OK “ will be displayed on the DRO and a “!” character will be returned on the serial interface. Only a limited number of characters are allowed and these are:  0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ=.#/-%  A space is also allowed.

Warning: The EEPROM will store any ASCII character but only a limited number of characters can be displayed. An ER=3 is returned if an improper value for the wheel ID is received. Character pacing of 25 ms minimum is also required for sending the data string.

### WEXITS

Return: END

Function: This command causes the program to exit the serial loop and return to normal manual operation.

### Error Codes

* ER = 1: Exceeded 2600 steps while homing. The wheel may be stuck or slipping.
* ER = 2: SBIG pulse is not in specification.
* ER = 3: Invalid Wheel ID.
* ER = 4: The Wheel failed to leave a position. The wheel may be stuck or slipping.
* ER = 5: Invalid position requested.
* ER = 6: The Wheel failed to reach a position. The wheel may be stuck or slipping.
* ER = 7: Invalid position requested for this wheel.
* ER = 8: No 12v power.
