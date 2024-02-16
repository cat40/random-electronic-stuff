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

## Okay, I've read everything but I still want to try it. How do I maximize my chance of success?


## footnotes
<sup>1</sup> In smart systems with a voltage regulator you will usually see an undershoot when the load is switched on and an overshoot when the load is switched off

