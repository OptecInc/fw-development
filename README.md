# Optec FilterWheel development

Optec, Inc. offers several different models of FilterWheel for the laboratory and astronomy communities. Here are links to resources for developing applications that use these Wheels.

## IFW / IFW2

The IFW and IFW2 use a serial protocol. This is included in the manual. There is also a Python class available here (<https://github.com/OptecInc/fw-python>) for reference.

Note that on linux you often need to give permission to access COM Ports. This is often achieved using the dialout group.

## HSFW

The HSFW uses USB HID for communication. To help with development Optec offers the following SDKs:

* .Net Framework and .Net Standard (<https://github.com/OptecInc/hsfw-dotnet-sdk>)
* C - built with hidapi (<https://github.com/OptecInc/hsfw-c-sdk>)
* Python (<https://github.com/OptecInc/fw-python>)

Note that for linux you need to give permission before using USB devices. A sample Udev rules file (50-usb-hsfw.rules) is available in this repository.
