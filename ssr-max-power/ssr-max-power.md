# How to calculate the maximum power your SSR can support

## tl;dr
```math
max\_power=duty\_cycle=(\frac{I_{limit}}{I_{load}})^2
```

## Introduction
SSRs are often specified by the maximum current they can pass without taking damage. However, this specification is generally based on the assumption that you are using the heatsink, and a hefty derate applies when you are not.

**Note:** This math does not apply to non-zero-crossing (SCR) relays. See <sup>3 4</sup>.

## How to determine the maximum RMS power your SSR can support

### Derate curves
Every SSR should have a datasheet, which will include a derate curve that looks like this:
![SSR derate curve](images/ssr_derate.png)

(this is from the Omron G3NA-210B-UTU-DC5-24 datasheet, found [here](hhttps://assets.omron.com/m/453bbd7a38a218b5/original/G3NA-Series-Solid-State-Relay-Datasheet.pdf))

For this particular relay, while it is nominally a 10A relay, it actually only supports 4A without the heatsink.

### mathy stuffs

First we will calculate the maximum power the SSR can support<sup>1</sup>. This is based on its rated current and your mains voltage (generally 120V or 230V nominal, depending on location). Power=current\*voltage. As an example for a 750W heater, assuming 120V nominal:
```math
P=IV
```
```math
P=4A\cdot 120V
```
```math
P=480W
```
This is about 64% of the heater mat's power. However, while we could just set the maximum duty cycle in the Klipper config to 0.64, we can actually get a bit more power though the magic of RMS.

RMS stands for Root Mean Square and is essentially a fancy pile of math that gets you the equivilent DC voltage or current of a periodic waveform, like the PWM signal sent by the mainboard to switch the heater. You can think of this as sort of the conceptual average of the wave<sup>2</sup>, though it is not the mathematical average.

Long story short, the RMS voltage calculation for a square wave with a given duty cycle is $A_{peak}\cdot\sqrt(duty_cycle)$ , where the duty cycle is expressed as a decimal between 0 and 1, and $A_{peak}$ is the maximum amplitude<sup>3</sup> of the square wave (in other words, the "high" value, when we set the low value to 0). Because we we are looking at current, we can redefine $A_{peak}$ as $I_{load}$ , and because $P=IV$ we can conclude $I_{load}=P/V$ . Based on this, we can do some mathy stuff to determine the maximum duty cycle we can set without overloading the relay:

Where $I_{limit}$ is the maximum current supported by the relay
```math
I_{rms}=I_{peak}\cdot\sqrt(duty\_cycle)
```
```math
\frac{I_{rms}}{I_{peak}}=\sqrt(duty\_cycle)
```
```math
duty\_cycle=(\frac{I_{rms}}{I_{peak}})^2
```

Now with example numbers, for a 4A rated relay, 750W bed, and 120V mains

```math
I_{rms}=4
```
```math
I_{peak}=\frac{750W}{120V}=6.25A
```
```math
4A=6.25A\cdot\sqrt(duty\_cycle)
```
```math
duty\_cycle=(\frac{4A}{6.25A})^2
```

## Footnotes
<sup>1</sup> It is important to remember that the SSR is not dissipating this power. This calculation is the maximum power of the load that the SSR switches.

<sup>2</sup> The actual average is different from the RMS, and generally less useful.

<sup>3</sup> You may note that the "peak" AC current value I'm using is in fact RMS. This is because I'm treating the waveform as DC (as you often can with AC RMS), which I can do because the relay only switches at zero-crossings so we can assume the RMS value is constant (the RMS value of a half-cycle is the same as a full sine wave cycle). This is still a bit of a liberty because I didn't convert from continuious to a discrete set of duty cycles, but it's okay because the relay does that automatically.

<sup>4</sup> As explained in footnote 3, some of the math here relies on the assumption that the only switches are at the zero-crossings. If you were to switch at arbitrary points during the wave, you will need to do much more complex math. See this [stackexchange answer](https://electronics.stackexchange.com/a/172623) for more details.
