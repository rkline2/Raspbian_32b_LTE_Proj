# Log 0: [](https://youtu.be/OEvjV1jtvl4)

This is the beginning of my journey in writing up "*bare metal*" code on a
raspberry pi 0w. There's no code in this log, but there are important pieces of
information that needs to be recorded.


## Hardware Requirements

Based on all of the tutorials I've seen on writing "bare metal" code, almost
all of them require a `64 bit (ARM v8 or greater)` processor which the pi v0
does not have.  

 CPU Info:
 ```
 processor       : 0
 model name      : ARMv6-compatible processor rev 7 (v6l)
 BogoMIPS        : 697.95
 Features        : half thumb fastmult vfp edsp java tls
 CPU implementer : 0x41
 CPU architecture: 7
 CPU variant     : 0x0
 CPU part        : 0xb76
 CPU revision    : 7

 Hardware        : BCM2835
 Revision        : 9000c1
 Serial          : 00000000cc69374b
 Model           : Raspberry Pi Zero W Rev 1.1
 ```

Fortunately, I found some solid resources to help me out with this
type of processor that date back to 2012. The links can be found in the
**Important References** section. They say the tutorials support Raspberry
devices all the way back to Model A! I should give a more in-depth analysis on
them in future logs.

## Important References

* **arm-tutorial-rpi:** https://github.com/BrianSidebotham/arm-tutorial-rpi
* **Baking Pi – Operating Systems Development**: https://www.cl.cam.ac.uk/projects/raspberrypi/tutorials/os/
* **BCM2835_datasheet_errata**: https://elinux.org/BCM2835_datasheet_errata


## Who do I talk to?

* Name: Rooklyn Kline
* Email: rkline2@umbc.edu
