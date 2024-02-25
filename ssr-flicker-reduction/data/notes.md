**Notes gathered when trying to reduce flicker**

TLDR
- it doesn't seem possible to make a badly flickering light not flicker by setting PWM settings tried during testing
- LED filament lights seem to flicker less than LED chip emitter lights
- Higher wattage LED lights tend to flicker more than lower wattage
- Using 44.9Hz and 47.9Hz reduces flickering but does not eliminate it, and the improvement isn't that drastic by eye

Methodology for determinging Flicker %
- Turn on bed heating at the appropraite test settings
- Using the oscilloscope measurement funection, measure the DC RMS value of the output of the phototransistor circuit
- Set horizontal divisions to 20ms
- Determine the difference in peak voltage observed using cursors on scope
- Flicker% = (voltage_diff)/(DC RMS Voltage)
