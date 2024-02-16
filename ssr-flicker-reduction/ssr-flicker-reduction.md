# Reducing flicker from your bed

## tl;dr
Sorry, you have to read the whole thing this time, to understand what you are getting into

## Why flicker happens

* A large load like a 3d printer bed causes a significant disruption to the power supply when it is switched. Usually you will see a voltage drop in a dumb system like mains electrical<sup>1</sup>.
* If there are lights on the circuit, the voltage drop pulses can cause the light to lower in brightness when the bed is on, and raise in brightness when the bed is off.

## Common methods of reducing flicker

* Inlet filter
    - An inlet filter will filter out minor changes in voltage and prevent them from feeding back onto the mains circuit. However, most are designed to filter out much higher frequencies that the frequency that causes the flicker
* Setting the PWM frequency of the bed controller to the mains frequency
    - This is not recommended.
    - See common misconceptions below

## Common misconceptions

* Setting the SSR to the mains frequency will reduce flicker
    - to my knowledge, there is no magical property about setting the pwm frequency to the mains frequency that reduces flicker. Rather, by design, mains frequency is around the point where human eyes are unable to see flicker any more, so for people who are not particularly sensitive to flicker, this may appear to be a solution.
    - This has significant drawbacks. Mainly the PID controller for the bed can become unstable<sup>2</sup>
* If you set the bed pwn frequency to the mains frequency the relay can become locked on or off
    - This may be true if you set the frequency to *twice* the mains frequency and get really unlucky. The pwm period and the mains period must be very close for this to happen, and they must have a particular phase difference.
    - Usually any ssr related issues are caused by something else. See above about PID instability as well as footnote 2.

## Okay, I've read everything but I still want to try it. How do I maximize my chance of success?

* First, set your period to be different from your mains frequency, ***but not higher***. For whatever reason, this seems to help a bit.
    - If you set the period to above your mains frequency, especially if you set it to above twice your mains frequency, the ssr will not really follow the PID instructions and bizarre behavior will occur (todo: test and verify)
* After you change the frequency, do a PID tune and make sure to save it.
    - If the tune fails, try tuning to a lower temperature, saving, and then tuning at the high temperature. In rare cases three steps may be necessary.
* Watch the heat graph closely for signs of instability the first few times you heat the bed afterwards.

## footnotes
<sup>1</sup> In smart systems with a voltage regulator you will usually see an undershoot when the load is switched on and an overshoot when the load is switched off

<sup>2</sup> todo write a bit about lowering resolution causing problems
