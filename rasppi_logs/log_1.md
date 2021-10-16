# Log 1: Working when I could've been eating a [Blueberry Muffin](https://youtu.be/kkZtm6DlON8?t=94)

When working throughout the tutorial I [mentioned](https://github.com/BrianSidebotham/arm-tutorial-rpi/tree/master/part-1) in my previous log, I came to discover that the "hello world" version of bare metal programming doesn't work for Raspberry Pi 0w...

***C h e c k***

Good news in all of this is that I learned a **LOT** about the Raspberry Pi 0w Processor. I'll provide a list of solid references/repos to check up on.


## The Issue
`ARM LED` didn't light up at all when compiling my C code to a `kernel.img`. This basically means the rpi 0w had an issue with the `.img`


## My Theory

Based on looking at the rpi 0w schematics, the `GPIO10` (General purpose input-output) connector doesn't connect to the `Status "ACT" LED` like the tutorial promised.

```
Models A and B provide GPIO access to the ACT status LED using GPIO 16.
Models A+ and B+ provide GPIO access to the ACT status LED using GPIO 47,
and the power status LED using GPIO 35  
```
    source: https://en.wikipedia.org/wiki/Raspberry_Pi#General_purpose_input-output_(GPIO)_connector    

Although I do not actually know if this is the cause of my issue because I cannot connect the RaspPi to a monitor (aka. no information/output at *all*) at the moment since it requires a hdmi mini (not micro) cable, it's safe to say that the `ARMv6` chip does not connect to the `ARM LED` with any `GPIO` connectors. When I say `ARMv6`, I actually mean the processor not its other components.      

## Son, It's Time to Talk about the ARMv6 Chip...
The `ARMv6` chip actually has the `Broadcom BCM2835 SoC`, `OnBoard 512 MB RAM` and `Dual Core VideoCore IV GPU` inside of it. *Why should I know this?* you might ask. The answer is *You don't! But it's still cool to know*.


-----------


## Important References

* **Raspberry Pi 0w Schematics:** https://www.raspberrypi.org/documentation/hardware/raspberrypi/schematics/rpi_SCH_ZeroW_1p1_reduced.pdf
* **Linux Kernel:** https://github.com/raspberrypi/linux/tree/rpi-5.10.y/kernel
* **DPI (Parallel Display Interface)**: https://www.raspberrypi.org/documentation/hardware/raspberrypi/dpi/README.md
* **RPi BCM2835 GPIOs**: https://elinux.org/RPi_BCM2835_GPIOs#GPIO16
* **BCM2835 datasheet errata**: https://elinux.org/BCM2835_datasheet_errata
* **Helpful YouTube Video on Rpi0w Schematics**: https://youtu.be/oq7JKRsrX-0
* **R-Pi Troubleshooting**: https://elinux.org/R-Pi_Troubleshooting#Red_power_LED_is_on.2C_green_LED_does_not_flash.2C_nothing_on_display
* **Raspberry_Pi#Connectors**: https://en.wikipedia.org/wiki/Raspberry_Pi#Connectors
* **4G bits DDR2 Mobile RAM™ PoP**: https://cdn-shop.adafruit.com/product-files/2885/E1775E40.pdf
* **VideoCore® IV 3D Architecture Reference Guide**: https://docs.broadcom.com/doc/12358545
* **Cool Info About the RaspPi 0w**: https://raspberry-projects.com/pi/category/pi-hardware/raspberry-pi-zero

## Who do I talk to?

* Name: Rooklyn Kline
* Email: rkline2@umbc.edu
