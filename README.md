## Introduction:<img width="1843" height="1543" alt="front_3D" src="https://github.com/user-attachments/assets/0ce40065-ffe4-4ef1-ae28-ccc8754a1a7a" />

This ESP32-C2 Based board is designed to control up to 5 channels of an LED Strip. Each channel is in theory capable of 4A up to 24V with the total current drawn from the board not exceeding 5A. Although in theory there isn't much preventing it from reaching 8A current(eFuse max) other than trace width and the bulk capacitor and so on.
Mosfet remains below 50c with a 99% duty cycle at 2.4A/24v @ 25KHz in testing. In theory, according to my calculations, it can easily handle 4A or even 4.5A/5A. above 4A is not recommended. It is compatible with Matter (using the code I'm too eepy and busy to upload right now) and HA with ESPHome. If you use HA  you might as well save yourself the trouble and use ESPHome as Matter can have it's own shortcomings.

Measured Channel FET rise time: 12.5ns.

eFuse can be skipped by shorting the VIN to EFUSE to the output with a wire.

The board is designed for 25KHz in mind but can be used with a lower or higher frequency within reason.

You can leave unused channnels empty and not solder them to save on cost. 

The EFUSE is connfigured to be triggered at 5.51A. It features a 150ms-300ms~ soft-start to prevent sparks when connecting the power.

Note: It features a 0201 test LED originally used as a fun challenge for soldering. I suggest changing it to a 0602/0402 package if using it in practice or debugging with it as it can be very challenging to solder.

A IPEX connector is used to debug and monitor the 3.3v rail ripple and transient performance. Note however that the 50 ohm termination seems to not be working, I will confirm why when the project is finished as it's not essential and works perfectly fine with a probe tip to BNC adapter as the probe is designed to be purposely lossy and cancel ringing. A BNC to IPEX Cable is recommended. Note that IPEX connectors are not meant for frequent unplugging and replugging. The socket is rated for 30-50 mating cycles

### Notes:
Frequency of 2.2MHz was chosen for the 3.3v rail to improve transient response and performance/size of the buck converter. Efficiency is not a big concern for such an application.
An eFuse (Hot-swap controller) was chosen for this board to prevent sparking upon plugging in and to reduce the required footprint for an ressetable poly fuse that can withstand 40-30v at 5A.


## Potential  Improvemtns:
- [ ] Add a factory reset button seperate from BOOT
- [ ] External antenna instead of built-in PCB
- [ ] Switch from ESP32-C2 to C3 or similiar for better matter compatbility and performance.
- [ ] Use a dedicated ESP32 IC instead of a pre-made module as the PCB is already 4 layers hence the impedance matching is very easy and does not add additional cost.
- [ ] Add a polymer/tantalum bulk cap for esp32 to reduce wifi transmission transients. This will require some consideration to prevent ringing at the output.
- [ ] Calculate and confirm feed-forward capacitor for the 3.3v rail. (It is picked based on gut feeling)
- [ ] Improve hand-solderability, use bigger TVS diodes.
- [ ] Add jumper for 3.3v from programming header.
- [ ] (?) Debug LED for each channel
- [ ] (?) RGB Indicator LED for when WiFI is connected and device is commisioned.
- [ ] (?) Software based SSFM solution for each channel to reduce EMI emitted from the LED Strips as they are difficult to shield and user assembled. For a simpler but less effective solution, Each channel can operate at a slightly different ferquency.
- [ ] (?) eFuse skip jumper.
