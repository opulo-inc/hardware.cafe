---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

# <span class="badge badge-primary">Github CI</span>
#<span class="badge badge-secondary">Web Service</span>
#<span class="badge badge-success">Open Source</span>
#<span class="badge badge-danger">Paid Service</span>
#<span class="badge badge-info">Free Service</span>

title: "Design to Pass"
layout: single

---

## Summary

Passing EMC testing can be made much easier by considering passing early on in the design phase. With proper engineering considerations, it's possible to pass your certification tests on your first attempt.

## PCB Design

### Radiated EMC

- Avoid long skinny copper pours. These can act as antennas and cause issues for both emissions and immunity.
    ![](https://private-user-images.githubusercontent.com/108100309/294284413-090990e6-05a9-4ef6-b464-5ee91ce8b9f8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NTIwMTA1MDMsIm5iZiI6MTc1MjAxMDIwMywicGF0aCI6Ii8xMDgxMDAzMDkvMjk0Mjg0NDEzLTA5MDk5MGU2LTA1YTktNGVmNi1iNDY0LTVlZTkxY2U4YjlmOC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjUwNzA4JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI1MDcwOFQyMTMwMDNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04N2ZjYWVlZjc4YTBiOTk2MmU1NmFiMjEwNGQwNGY1NGQ3MDJmMjcxNDY2NjM3OWEzZmIwOGFkMWM4MWYzZmQ4JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.1a1CMEeOrW1QDzRQKkWuMqoEkaCdcnvICENxPIrT5HI)
    *Remove these artifacts wherever possible*
- Use at least four layers, and keep one of them as a full, uninterrupted ground pour. Ideally use a ground pour on your signal layers as well.
- Keep all traces with high switching frequencies as short as possible. These are commonly found in buck converters, where the higher current being switched makes this particularly bad for emissions.
- For motor or other high-power outputs, consider adding a ferrite bead inline. These can reduce high frequency signals on a high current line, which should greatly reduce any emissions for the frequencies that they attenuate.
- Enclose your PCB in a metal enclosure, ideally grounded. This will shield the board from interference, and also block a tremendous amount of emissions coming from the board.

### ESD

- Adding TVS (Transient Voltage Suppression) diodes on every single exposed line is a sure-fire way to protect against ESD. This includes both power and signal lines. There are dedicated TVS diodes with clamping voltages for specific electrical standards, like USB or RS-485. Check the schematic below to see TVS diodes being used to clamp some exposed I/O pins and power lines.

    <kicanvas-embed src="https://raw.githubusercontent.com/opulo-inc/lumenpnp/main/pnp/pcb/mobo/microcontroller.kicad_sch" controls="full"> </kicanvas-embed>

- Whether USB shields should be connected to ground is a [hotly debated topic](https://electronics.stackexchange.com/questions/661902/usb-shielding-device-or-host-side) in terms of best practice. A great in-between solve is putting a 0 ohm resistor footprint connecting the shield to ground, and choose to either populate or DNP as a result of testing. There are EMC and ESD considerations around this decision, so it might be best to make the edit during testing based on what'll help you pass.
- Keeping your controller isolated in a plastic enclosure will make it very hard to fail ESD testing. If the probe can't reach the board, you've effectively defeated the test. Alternatively, you can enclose the board in a metal, grounded box which also doubles as some RE shielding.

## Cabling

Cabling can be an issue particualarly for RE tests. Certain lengths of cables act as excellent antennas and are prone to kick out electromagnetic interference, especially if there's high current and high switching speeds running through them. In RE tests, cable emissions typically show up around the 30MHz - 70MHz range. If you see spikes there, it's likely your cabling.

![](https://emcfastpass.com/wp-content/uploads/2014/12/re_v1.gif)
*Spikes around here are likely a result of cabling*

The best way to eliminate emissions from your cable runs is to shield your cable harnesses, and ideally ground your shielding as well. Your PCB can also have circuitry that attenuates any high-frequency noise which will help as well.

Power cables can also show an emissions spike in the 30MHz - 40MHz range. A common solve is adding a clamp-on ferrite bead which can attenuate these emissions, and they're easy to swap for testing

![](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/A_collection_of_Snap-On_-_Clamp-on_ferrite_beads.jpg/1920px-A_collection_of_Snap-On_-_Clamp-on_ferrite_beads.jpg)
*[By Unconventional2 - Own work, CC BY-SA 4.0](https://commons.wikimedia.org/w/index.php?curid=43384001)*

## Power Supply

If at all possible, choose to use an off-the-shelf power supply brick or module. These are designed to pass Conducted Emissions and Conducted Immunity testing, and should be an easy way to ensure your device passes without issue.

![](https://upload.wikimedia.org/wikipedia/commons/2/2d/Notebook-Computer-AC-Adapter.jpg)
*A power brick that provides DC power for your product*

![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/1f/Mean_Well_HRP-100_smps.jpg/1280px-Mean_Well_HRP-100_smps.jpg)
*A MeanWell power supply meant to be integrated into an end product - [By Phiarc - Own work, CC BY-SA 4.0](https://commons.wikimedia.org/w/index.php?curid=122682748)*


## Software

Although the vast majority of EMC tests are related to your device's hardware, RI in particular can be made easier to pass with some software updates.

Many standards only require that a device will continue normal operation, or resume normal operation if it's interrupted during RI testing. This means that adding some software checks to ensure a restart or reconnection in the case of issues can mean the difference between passing and failing.

For example, if your device's standard operating mode involves a serial communication between a computer and a microcontroller, having consistent checks for serial data integrity and re-establishing connection in the case of an error can make any interference not an issue.