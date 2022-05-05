# 3D Modeling and Printing

### Process
1. Design or download a model (.stl file)
2. Import the stl file(s) to slicing software (e.g. IdeaMaker)
3. Slice the object
4. Slicing takes the model and does the math on it to create gcode instructions for the 3D printer
5. Export the gcode instructions to a usb drive or SD card depending on the printer
6. Plug in drive to printer and begin the 3D print

### Notes
- PLA is a common plastic used b/c it is softer (less wear & tear on printer) and needs less heat to be melted
- ABS is a harder plastic that is used and thus requires more heat to melt it
- A variety of different filaments can be used to print things
- Tiny errors in a 3D printer’s movement results in big errors with the print b/c movements are done hundreds of times

# Raspberry Pi

### Board Structure
- Set of GPIO pins (General purpose input-output pins) [Read More](https://www.raspberrypi.org/documentation/usage/gpio/)
- Serial pin on TX (GPIO14) and RX (GPIO15)
- Can print out [this](https://github.com/splitbrain/rpibplusleaf) and place on pi for reference
- [Interactive GPIO Guide](https://pinout.xyz/)

### Pi Camera
- Watch out, static can kill it
- FIX PI CAMERA DETECTION ERROR by enabling the I2C Interface in preferences --> raspberry pi configuration