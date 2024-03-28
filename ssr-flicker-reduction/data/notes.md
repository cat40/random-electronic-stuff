**Notes gathered when trying to reduce flicker**

TLDR
- Changing PWM frequency can have effects on lights flickering and bed heating
- 44.9Hz and 47.9Hz can reduce light flickering
- **Under no circumstances should you try to match grid frequency!!**
- Higher wattage LED lights tend to flicker more than lower wattage
- Some lamps do not change flicker at different PWM frequencies (GE Relax for example).

Methodology for determinging Flicker %
- Turn on bed heating at the appropraite test settings
- Using the oscilloscope measurement funection, measure the DC RMS value of the output of the phototransistor circuit
- Set horizontal divisions to 20ms
- Determine the difference in peak voltage observed using cursors on scope
- Flicker% = (voltage_peak_diff)/(DC RMS Voltage)
- Used PWM cycle times of 0.1 (10Hz), 0.02227 (44.9Hz), 0.02088 (47.9Hz)

- Thanks ark for picking these frequencies!
