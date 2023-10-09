# Electrical Debugging Tips
In no particular order, though ones closer to the top tend to be more important in my eyes

* RTFD. Read the datasheet. Then read it again.
    - You don't have to read it cover to cover (only interns really do that), but make use of the table of contents and find function in your PDF viewer to locate the relevant sections
    - If you're working with a chip for a long time, it's sometimes helpful to print a hard copy and highlight/annotate it.
* Check connections first. Make sure they are physically secure, and verify continuity or preferably resistance.
* If it ever worked, look for what's changed since the last time it worked. That's likely to be related (especially if the magic smoke or zappy-zappy going where it shouldn't has happened)
* There is an optimization to be found between testing what is likely to be the problem, and testing what is easy/safe to test. What side you lean towards depends on the particular circumstances and your personal work style.
* Testing should be repeatable. If you get a strange result, check again, and keep checking until your result is mostly consistent. If it never gets consistent, consider measuring/testing something else.
    - Your eyes can lie to you. Even if it looks connected, measure it to be sure. Visual inspection is good for FOD (Foreign Object Debris) and totally miswired stuff but not much beyond that.
    - Your instruments can lie to you. When you see something you don't expect, check the measurement first if it's easy to do so (this one is a little subjective and dependent on circumstances)
