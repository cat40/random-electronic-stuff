# Electrical Debugging

## General Procedure
1. Identify the problem. What is the thing doing that's it's not supposed to be doing, or what is it not doing that it's supposed to be doing?
1. Remove any safety hazards. If the printer is on fire, it's usually best to put it out before proceeding further.
    1. Pay careful attention to mains voltage. You should not debug your printer with the mains power connected. Unplug, then debug.
1. Reproduce the problem, if safe to do so. Try to come up with a minimal system where the problem still occurs. In other words, remove variables.
    1. Do ***NOT*** attempt to reproduce a problem where a power fault may be present, especially for mains.

## Electrical Debugging Tips
In no particular order, though ones closer to the top tend to be more important in my eyes

* Assume nothing. Not even your own name.
* RTFD. Read the datasheet. Then read it again.
    - You don't have to read it cover to cover (only interns really do that), but make use of the table of contents and find function in your PDF viewer to locate the relevant sections
    - If you're working with a chip for a long time, it's sometimes helpful to print a hard copy and highlight/annotate it.
        - This is doubly true for LT power converter datasheets. They like to solve their equations for less than helpful variables.
* RTFS. Read the schematic, if available. Often, the answer to your question or problem lies there. At the very least, understanding the system is necessary to debug it, and the schematic is tremendously helpful in understanding the system.
* Check connections first. Make sure they are physically secure, and verify continuity or preferably resistance.
* If it ever worked, look for what's changed since the last time it worked. That's likely to be related (especially if the magic smoke or zappy-zappy going where it shouldn't has happened)
* There is an optimization to be found between testing what is likely to be the problem, and testing what is easy/safe to test. What side you lean towards depends on the particular circumstances and your personal work style.
* Testing should be repeatable. If you get a strange result, check again, and keep checking until your result is mostly consistent. If it never gets consistent, consider measuring/testing something else.
* Your eyes can lie to you. Even if it looks connected, measure it to be sure. Visual inspection is good for FOD (Foreign Object Debris) and totally miswired stuff but not much beyond that. Use your meter (unless you found some ladybugs or something. Meters don't work too well on those).
* Your instruments can lie to you. When you see something you don't expect, check the measurement first if it's easy to do so (this one is a little subjective and dependent on circumstances)
    - Make sure you are using your instrument right. The probes go on the wires, not up your nose, and that sort of thing, y'know? Especially check that your meter is in the right mode and range.
    - Check the test and make sure it's inducing the right conditions and measuring the right data. Don't eat the cookies to check if the brownies are done.
* Suspect the hardware, and suspect the test.

## Further Reading
* https://github.com/cmdremily/BoronTrident/blob/master/electronics/donts.md is an excellent resource for how not to break things, while debugging or otherwise.
