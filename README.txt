Exar USB Serial Driver
======================
#### Version 1C-AK  2023/03/17
* Fix errors in code.
* Update to work with kernel 5.15+

Version 1C  2017/1/11
        Add the 9-bit mode support.
        Disbale the debug messages.
Version 1B, 11/6/2015
Fixed Bug: The conditional logic to support kernel 3.9 was incorrect(line 396 in xr_usb_serial_common.c). 

Version 1A, 1/9/2015

This driver will work with any USB UART function in these Exar devices:
	XR21V1410/1412/1414
	XR21B1411
	XR21B1420/1422/1424
	XR22801/802/804

The source code has been tested on various Linux kernels from 3.6.x to 3.17.x.  
This may also work with newer kernels as well.  


Installation
------------

* Compile and install the common usb serial driver module

	# make
	# insmod ./xr_usb_serial_common.ko


* Alternativley install via DKMS

    # cp -a ../$(basename $(pwd)) /usr/src/xr_usb_serial_common-1c
    # dkms add -m xr_usb_serial_common -v 1c
    # dkms build -m xr_usb_serial_common -v 1c
    # dkms install -m xr_usb_serial_common -v 1c


* Ensure that the cdc-acm module is not loaded (assumig that it is not needed)

    # echo blacklist cdc-acm > /etc/modprobe.d/blacklist-cdc-acm.conf
    # update-initramfs -u


* Plug the device into the USB host.  You should see up to four devices created,
  typically /dev/ttyXRUSB[0-3].


Tips for Debugging
------------------

* Check that the USB UART is detected by the system

	# lsusb

* Check that the CDC-ACM driver was not installed for the Exar USB UART

	# ls /dev/tty*

	To remove the CDC-ACM driver and install the driver:

	# rmmod cdc-acm
	# modprobe -r usbserial
	# modprobe usbserial
	# insmod ./xr_usb_serial_common.ko


Technical Support
-----------------
Send any technical questions/issues to uarttechsupport@exar.com. 

