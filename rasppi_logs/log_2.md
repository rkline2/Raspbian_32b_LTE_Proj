# Log 2: I almost fell into [The Hooks](https://youtu.be/OlAZf1sv0TQ)

## Update from Previous Log
I managed to get the `rpi0w` to run the `Status ACT LED`. The issue I was having is that I did not properly format the `micro SD` card. I was attempting to run the rpi by naively putting in the compiled `kernel.img` and `config.txt` file into the empty `boot` file. Looking back, this obviously doesn't make any sense. Why did I decide to do that? Anyways, I put the compiled files into the latest `Raspberry Pi OS Lite` `boot/`  file and replaced any of the existing files respectively (would recommend keeping them and just changing the name).       


***Moving On***


## The Slippery Slope of the rpi0w Wifi Chip

"Now that I feel that I have a fundamental understanding of how firmware code works. I think it's time to dive into my main objective which is to investigate the wifi chip's firmware info. That way I can see if it's possible to [packet inject](https://en.wikipedia.org/wiki/Packet_injection)." - past me


Present me: *So this was a mistake...*

Firstly, I had no idea what I was doing. I fortunately didn't break any hardware because I didn't run any code. This was all pure research and trust me, that was enough work to keep a whole team busy. I researched on the wifi chip for a solid two weeks just to find some kind of clue that can help me out. I'm only going to mention the most important documents to save both of our times.

The wifi chip design is licensed from a Swedish company called [Proant](https://proantantennas.com/). While scrambling into their archives, I located the wifi chip's manual which contains a deep amount of information. I'm only going to reference pg's. 47 and 55 because I feel that they're the most important.

**Pg. 47**

```
11.3 GPIO Interface

Five general purpose I/O (GPIO) pins are available on the CYW43438 that
can be used to connect to various external devices.

GPIOs are tristated by default. Subsequently, they can be programmed to be
either input or output pins via the GPIO control register. They can also be
programmed to have internal pull-up or pull-down resistors.

GPIO_0 is normally used as a WL_HOST_WAKE signal.

The CYW43438 supports a 2-wire coexistence configuration using GPIO_1 and
GPIO_2.
```

**Pg. 55**

| Signal Name | WLBGA Ball | Type | Description
--- | --- | --- | ---
GPIO_0 | J6 | I/O | Programmable GPIO pins. This pin becomes an output pin when it is used as WLAN_HOST_WAKE/out-of-band signal.
GPIO_1 | H6 | I/O | Programmable GPIO pins
GPIO_2 | L5 | I/O | Programmable GPIO pins

***The only problem is, I had no idea what any of the information meant.***

I wanted to mess with the `GPIO_0` pin by sending a similar electrical pulse that was used by the `Status "ACT" LED` code I worked on earlier.

## The Issue

There's a saying that I live by, "we should exercise our curiosity with caution." I need another "nerd" on this besides myself to help translate what all of the information I provided means. I reached out to Alberto and explained to him my dilemma.

I think he started to understand that the task at hand was too overwhelming to handle. I personally think that this would be difficult for a senior developer to understand because the information is slowly diving into Electrical Engineering. Plus the only libraries I would have available is the [C Standard Library](https://www.tutorialspoint.com/c_standard_library/index.htm)! The time/effort that would have had to go into it isn't worth the small boost of efficiency. I need to find a less labor intensive solution to my overall objective.

## The Compromise

Nevertheless, instead of focusing on bare-metal coding, I've been assigned a new task that involves working on kernel-level code. The objective is still the same which is to research send a tcp packet from the `rpi-0w` to another device, but this time, I have an Operating System on my side to provide me many more available open source libraries.            

Good news in all of this is that I learned a **LOT** about the Raspberry Pi 0w Wifi Chip. I'll provide a list of solid references to check up on that may be of use. There's also a lot of other cool documents I found in the `resources/` directory. Feel free to check them out if you're interested.  


-----------


## Important References

* [**Raspberry Pi 0w Wifi Chip Manual**](resources/002-14796_YW43438_Single-Chip_IEEE_802.11_b_g_n_MAC_Baseband_Radio_with_Integrated_Bluetooth_5.1_Compliance.pdf)

* [**ARM Architecture Reference Manual**](resources/DDI0406C_arm_architecture_reference_manual.pdf)

* [**ARM and Thumb-2 Instruction Set Quick Reference Card**](resources/QRC0001_UAL.pdf)

* [**Raspberry Pi Zero W external antenna mod**](https://www.briandorey.com/post/raspberry-pi-zero-w-external-antenna-mod)


## Who do I talk to?

* Name: Rooklyn Kline
* Email: rkline2@umbc.edu
