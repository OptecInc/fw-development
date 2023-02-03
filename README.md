# Optec FilterWheel development

Optec, Inc. offers several different models of FilterWheel for laboratory and astronomy applications. Here are links to resources for developing applications that use these FilterWheels.

## IFW / IFW2

The IFW and IFW2 use a serial protocol for control. This is included in the [IFW-Serial.md](IFW-Serial.md) file. There is also a Python class for scripting and automation available here: <https://github.com/OptecInc/fw-python>. The Python class can be used as a reference to help develop applications in other languages.

Note that on Linux you often need to give permission to access Serial Ports. This is often achieved using the dialout group.

## HSFW

The HSFW uses USB HID for communication. Because HID is often more difficult to develop for Optec offers the following SDKs:

* .Net Framework and .Net Standard: <https://github.com/OptecInc/hsfw-dotnet-sdk>. The .Net Standard version supports Windows, Linux and macOS.
* C - uses hidapi for communication. Tested on Windows, Linux and macOS. <https://github.com/OptecInc/hsfw-c-sdk>
* Python 3: <https://github.com/OptecInc/fw-python>

Note that for Linux you often need to give permission before using USB devices. A sample Udev rules file [50-usb-hsfw.rules](50-usb-hsfw.rules) is available in this repository.
