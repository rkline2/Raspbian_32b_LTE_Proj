# Log 3: Last log, let's make it [Count](https://youtu.be/atk57eE6ewg)

## Summary
I'm gonna keep this log short and simple. I'm assuming whoever is reading this just skipped to the end to see the final result. I would probably do the same, so no hard feelings ;).

Overall, after following a paper trail of different firmware/kernel packages, I came across a specific flavor of Kali Linux that allows the `Raspberry Pi 0w (rpi 0w)` to go into [monitor mode](https://en.wikipedia.org/wiki/Monitor_mode) and [packet injection](https://en.wikipedia.org/wiki/Packet_injection) with a few simple commands. All of the necessary code is already pre-packed in the Operating System. I will provide more details on the OS a little later on.

Throughout this research process, I didn't create any code so all of the work is public knowledge, so I don't care about showing this to anyone since you can find this all on the internet. The steps to implement `monitor mode` and `packet injection` on the `rpi 0w` are pretty straight forward. All you need to do is, ***install the OS -> copy commands -> paste it -> DONE***. Can't get any easier than this.      

## Looking for Copper, Struck Gold

I'll be going over the libraries I discovered then I'll go over the solution near the end.  

### Picolibc
After receiving new instructions on working on kernel level code rather than bare-metal, I began looking into a library that might be of use to me called `picolibc` (info about it [here](https://www.cnx-software.com/2019/10/03/picolibc-lightweight-c-library-embedded-systems/)). Overall, it's a solid little library that gives developers way more libraries than the [C Standard Library](https://www.tutorialspoint.com/c_standard_library/index.htm). Remember, when working down to the bare-metal or super tiny computers like the Raspberry Pi, you're only provided the C Standard Library to work on. `Picolibc` utilizes the same libraries as `newlibc` (more info [here](https://sourceware.org/newlib/)), but is hyper efficient in memory. This means you can run this code with a very small capacity of RAM/ROM.

    Source Repo: https://github.com/picolibc/picolibc

### The Big Picture (Intermission)
Even though I was supposed to have monitor mode/packet injection specifically work on `rpi 0w`, I wanted this to also work on more common devices. I feel that sometimes develops get so focused into the minor details that they loose touch with realism.

Most people don't have raspberry pi's sitting around in their houses. They have smart devices like smart fridges or smart thermostats (literally anything that's connected to the internet). Even though the raspberry pi 0w is $5 in most retailers, I don't see anyone getting enthused about a device that looks like a remote detonator. That's why I feel that Nexmon may provide me the solution to these problems.

### Nexmon
Nexmon is a solid library that I highly recommend using if you're looking into utilizing firmware patches. The OS kernel I used to solve the project `re4son-kernel` utilizes this library as a module. Don't believe me, see for [yourself](https://re4son-kernel.com/re4son-pi-kernel/). It prevents you from diving into the bare-metal code that I had to go through in my previous iterations. I encountered some installation troubles on the raspberry pi under a Debian OS, but I didn't dive too deep into it because I found an alternative solution. I recommend taking a look at the source-code's README.md file for a more detailed description of the firmware patch can do.   

    Source Repo: https://github.com/seemoo-lab/nexmon

### Res4son kernel
I'm not sure if you're catching the trend or not, but we're diving more into more well-known libraries. Can you predict what the next open-source software will be? Me neither! Well, when I was investigating this library I didn't, but you'll soon understand why I included this library later on. "You can't connect the dots looking forward; you can only connect them looking backwards. So you have to trust that the dots will somehow connect in your future." - Steve Jobs    

    Source Repo: https://github.com/Re4son/re4son-kernel-builder

### Kali Linux Rpi0w Nexmon-lite
Does this OS look familiar to you? Yep that's right! It utilizes the `Nexmon` firmware patch I previously mentioned. There's something that you may not have catched, it also uses the latest `ke4son-kernel` how cool is that! So there is some method to my madness.

**Note** if you try to install the default version on the kali linux webpage, you will probably get the desktop version. If you want that, then that's fine.

    OS Info: https://www.kali.org/docs/arm/raspberry-pi-zero-w/

Specifically for the `rpi 0w` you probably want the non-desktop version. Fortunately, they have that. I provided links to the install directory below if you want to do it yourself, but you can also copy and paste the commands if you want the latest version. Please read the README.md file if you're going to install this repo. It actually contains important information.  

    Source Repo: https://gitlab.com/kalilinux/build-scripts/kali-arm

**Note** This script will only work under a linux environment NOT MAC or Windows. I ran it under Ubuntu VM and it was fine, but try to use  Kali Linux 32-bit and 64-bit installations if you can.  

```
git clone https://gitlab.com/kalilinux/build-scripts/kali-arm

./build-deps.sh
./rpi0w-nexmon-minimal.sh latest

```

### StickyFingers Kali Pi armel [](https://youtu.be/79zA85gyi1c?t=76)
This is the solution that I decided to go on. The operationg system comes pre-packaged with all of the necessary tools you need to run a `rpi 0w` into monitor mode and packet inject. The installation process is fairly straight forward. You just burn the installed image into you micro sd card, plug it into your raspberry pi and you're good to go. Well, you have to enter a few commands first to get it up and running.

If you look closely at the link I provided, you can enable auto login if you want to, so it's possible for it to be a plug and play if that's what you're looking for. I'll it leave to you to play around with it.

    OS Info: https://whitedome.com.au/re4son/sticky-fingers-kali-pi-pre-installed-image/

**Note**: *The sticky fingers commands don't need to connect to the internet to run. SSH can be enabled/disabled. I provided some helpful links below if you don't know how to set it up*

Commands to run in monitor mode:

```
<!-- login as 'root' -->

sudo mon0up

airodump-ng mon0
```

Commands to run packet injection:

```
<!-- login as 'root' -->

sudo mon0up

aireplay-ng --test mon0
```

### What's next?
Even though I have won the battle, I have not won the war. I want these types of programs to work on more common devices. My next project is to have this work on cellphones. Particularly on phones that take a `micro SD` card. Even though my internship is almost ending, I'll be working on this on my own spare time. I really enjoy this kind of work, so I don't mind doing it for free.       


-----------


## Important References

* [**About PicoLibC**](https://www.cnx-software.com/2019/10/03/picolibc-lightweight-c-library-embedded-systems/)

* [**Full PicoLibC Video**](https://youtu.be/SC6aBezNFFQ)


* [**Re4son-Kernel for Raspberry Pi**](https://re4son-kernel.com/re4son-pi-kernel/)

* [**STICKY FINGER’S KALI-PI – Pre-installed**](https://whitedome.com.au/re4son/sticky-fingers-kali-pi-pre-installed-image/)

* [**Enable Monitor Mode & Packet Injection Tutorial**](https://null-byte.wonderhowto.com/how-to/enable-monitor-mode-packet-injection-raspberry-pi-0189378/)

* [**Some Helpful Commands to Connect to the Internet or SSH**](https://pastebin.com/s5E3ZyuN)  


## Who do I talk to?

* Name: Rooklyn Kline
* Email: rkline2@umbc.edu
