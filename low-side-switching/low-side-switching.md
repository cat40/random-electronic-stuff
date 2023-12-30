# Low Side Switching
<sub>Note: some of this (especially terminology) has been slightly simplified and not all edge cases were accounted for, for the sake of clarity. I tried to retain accuracy and nuance everywhere it is important to understand the concepts. I figure if you're able to identify the changes, you probably don't need to be reading this anyway</sub>

## So what is it?

When you are switching an electronic load in a simple DC circuit, you have two options. You can switch the positive voltage going to the load (hereinafter, the supply), or you can switch the negative (or zero) voltage coming back from the load (hereinafter, the return). We call the former "high-side switching" and the latter "low-side switching".

If you prefer a visual illustration:

This is a high side switched circuit:

![high side circuit](images/high_side.png)


This is a low side switched circuit:

![low side circuit](images/low_side.png)


## But why? This seems stupid

On the surface, low-side switching seems like a terrible idea. After all, it leaves the load energized even when the switch is off! And in many cases we do switch the high side, for example, the light switches in most buildings. But low-side switching also has its advantages:

### Use with MOSFETs

Lots of times one might wish to switch a load automatically, rather than throwing a physical switch. There are various ways of accomplishing this, but one of the most common (on DC circuits) is a MOSFET. They can be used for many things, and the details of how they work are beyond the scope of this document.For the purposes of this document you can think of them as voltage controlled switches. They have three terminals, a drain, a gate, and a source. The drain is the "positive" terminal (higher voltage), source is the "negative" terminal (lower voltage), and the gate controls whether the switch is closed or open.

There are two<sup>1</sup> main types, N-chammel (NMOS) and P-channel (PMOS) (these are somewhat analogous to NPN and PNP BJTs). Generally (or at least conceptually) NMOS is used for low-side switching, and PMOS is used-for high side switching<sup>2</sup>. On an NMOS, the gate is referenced to the device's source, and on PMOS it's referenced to the drain. Importantly, *in neither case is the gate referenced to the global 0V net (often called GND)*. To turn on an NMOS, you have to drive the gate above the drain, which in this case means above the load's return. This is pretty easy. To turn on a PMOS, you have to drive the gate below the supply, which is less so. So we often like to use NMOS in a low-side configuration when possible.


### Variable supply voltages


## Ok, this has been fun and all, but why should I care?



<sup>1</sup> yes, yes, there are actually more like 4. For these writeup we'll assume the more common enhancement mode MOSFETs are being used

<sup>2</sup> to do it the other way you'd need to drive the gate outside the bounds of the supply voltage, which tends to be rather annoying
