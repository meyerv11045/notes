# I/O Systems

Input/Output (I/O) systems are used to connect a computer with external devices caled peripherals. Example devices for a personal computer include keyboards, monitors, printers, and wireless networks. Example devices for an embedded system include toaster's heating element, a toy's speech synthesizer, an engine's fuel injector, and a satellite's panel motors.

## Memory-mapped I/O
A method of communicating with input-output devices such as printers. Memory-mapped I/O involves dedicating a portion of the address space to I/O devices instead of memory. This allows a store to the specified address to send data to the device while a load from the address will receive data from the device.

The blow program writes the value 7 to a an I/O device at a specified memory address.
``` assembly
MOV R1, #7
LDR R2, =ioadr
STR R1, [R2]
ioadr DCD 0x20001000
```
To read from the the same device: `LDR R1, [R2]`

A **device driver** is software that communicates with an I/O device. They are often downloaded or installed for things such as printers since writing a device driver requires detailed knowledge about the I/O device hardware including the addresses and behavior of the memory mapped I/O registers. Other programs can access the device by making calls to functions in the device driver, therefore avoiding the need to understand the low-level device hardware. 

## Programmed I/O
Certain architectures, such as x86, use specialzied instructions instead of memory-mapped I/O to communicate with I/O devices.

``` assembly
LDRIO R1, device1
STRIO R2, device2
```

## Serial I/O
When a microcontroller needs to send more bits than free pins so it breaks the message into bits that it sends at each step. 
There are different standards for serial I/O:

- Serial Peripheral Interface (SPI)
    - Clocks synchronized btw sender and receiver
- Universal Asynchronous Receiver/Transmitter (UART)
    - Clocks unsychronizd btw sender and receiver
    - Uses the TX (transmit) and RX (receive) line on the pies
    - Signaling in units of baud instead of bits/sec since 8 data bits are sent using 10 symbols (a start and stop bit)
    - 9600 baud rate = 9600 symbols /sec = 960 bytes(chars)/sec
    - Slow compared to modern standards
- Universal Serial Bus (USB)
- Ethernet


Many embedded systems use analog I/O. Therefore they use analog-to-digital converters (ADCs) to turn analog signals (voltages) to digital values (bits) and they use digital-to-analog converters (DACs) to turn bits to voltages. ADCs are built into many microcontrollers but few have built-in DACs.

## Motors 
- Motors draw a very high current that can cause glitches on the power supply that disturb the digital logic
    - Problem is mitigated by using different power supply for motor
- DC and stepper motors require a high drive current so a powerful driver such as an H-bridge must be connected between the microcontroller and the motor
- **Stepper Motors** accept a sequence of pulses that each rotate the motor by a fixed angle called a step 
    - More precise position control
- **DC Motors** tend to spin at thousands of RPM at very low torque so gear trains are added at cost of decreased RPM but benefit of higher torque
    - Reversing the current makes the motor spin in the opposite direction
    - Changing the current abruptly will result in a large potentially damagaging voltage spike from the inductance of the motor's electromagnet
- H-bridges handle all the these current related details
    - Requires a seperate logic and motor power supply 
    - Supports coast, brake, reverse, and forward for DC motors
- **Servo Motor**
    - A DC motor integrated with a gear train and shaft encoder
    - Limited rotation (unless you get a continuous rotation servo)

