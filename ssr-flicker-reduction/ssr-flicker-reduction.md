# Reducing flicker from your bed

## tl;dr

The main way to reduce flicker is to adjust the pwm frequency to 44.9 or 47.9 Hz. Alternatively or additionally, chance your lamps to the ones recommended below. An example adjusted `heater_bed` config section:



## Why flicker happens

* A large load like a 3d printer bed causes a significant disruption to the power supply when it is switched. Usually you will see a voltage drop in a dumb system like mains electrical[^1].
* If there are lights on the circuit, the voltage drop pulses can cause the light to lower in brightness when the bed is on, and raise in brightness when the bed is off[^2].

Here's some actual data:

![sine wave with voltage drop](images/Phototransistor_capture_LED_Flickering.png)

(image credit Royicus)

Here you can see how the mains voltage near the printer drops when the bed is one.

A lamp was connected and a phototransistor was used to gauge the light output, and as you can see in these captures the output majorly fluctuates at the default 10Hz frequency:

![bad flicker phototransistor sine wave](images/phototransistor_output_worst_lamp_10Hz_pwm.png)

(image credit Royicus)

## Options for reducing flicker
### Change the bed-heater frequency to 44.9 or 47.9 Hz
**Note**: All frequencies discussed in this section are relative to a 60Hz mains system. If your mains frequency is 50Hz you will probably experience similar results adjusting the numbers proportionally, however, this has not been tested.

It seems that 44.9 or 48.9 Hz results in a sweet spot between reducing flicker and causing instability during heating (see below). To set this, simply add a line in the `[bed_heater]` section of your Klipper config: `cycle_time = 0.2227` (44.9 Hz) or `cycle_time = 0.020876` (47.9Hz). If you already have a `cycle_time` line simply change the number.


With this frequency applied you can see that the lamp brightness fluctuates far less:

![smoother sine wave](images/phototransistor_output_worst_lamp_49_9Hz_pwm.png)

(image credit Royicus)

Which of those two numbers works better seems to be variable, you can see more detailed data, credit Royicus, (here)[data]

#### Why you should not set the PWM frequency to or near your mains frequency
There is a decent chance you will get heating instability, such as:

![unstable bed heating graph](images/thor_instability1.png)

![also an unstable bed heating graph](images/thor_instability2.png)

(images taken at 60Hz, credit Thor)

The reason for this is the SSR only switches at zero-crossings, and if the switching frequency is close enough to the mains frequency the SSR can wind up getting sort of locked, where it can't control whether the power is fully on or half on, so the heating becomes erratic. You can see the problematic power waveform below;

![unstable ssr switching](images/ark_60hz_mains.jpg)

(image credit ark)

### Change to different light bulbs
* Lower power lightbulbs have been observed to flicker less, with the exception of 40W equivalent GE bulbs
* GE relax bulbs seem to perform the best of the ones tested, including GE classic, Lowe's store brand, and IKEA.

### Install an inlet filter
* Inlet filters are generally aimed at much higher frequencies that would not be observable to the human eye, and are unlikely to be effective at reducing flicker

## Attributions:
This was a major team effort on the Voron discord, but special recognition should go to:
* Voron discord user Royicus, for many scope captures and much testing
* Voron discord user ark, for coming up with the numbers and some scope captures showing the reasons for instability at mains frequency

[^1]: In smart systems with a voltage regulator you will usually see an undershoot when the load is switched on and an overshoot when the load is switched off

[^2]: LED and CFL lightbulbs won't behave *quite* that simply, but the end result is still flicker, based on the variation in RMS line voltage
