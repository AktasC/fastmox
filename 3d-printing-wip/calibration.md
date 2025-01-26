---
description: >-
  No-nonsense 3D printing calibration guide | Orca Slicer | Bambu Lab - P1S x
  AMS
---

# ⚙️ Calibration

## <mark style="color:purple;">W.I.P</mark>

Do these calibrations with the "0.20mm Standard" profile, _stop fµcking around kid_.

## Filament Calibration

**Don't forget to calibrate your printer first.**\
It's a good idea to make sure your belts are properly tensioned before attempting any calibration process. I know, it's a pain in the ass, but making sure the hardware is properly calibrated first will ensure you get valid, consistant and thus usable calibration results.

As I have a P1S, I'll follow these steps:&#x20;

* [ ] Check belts - retension if necessary
* [ ] Inspect carbon rods & Z-axis linear rods - _Wipe with Isopropanol every once in a while_
* [ ] Check Z-axis lubrication - _Clean & lubricate if necessary / if you see plastic debris stuck_
* [ ] Run the 30mn calibration process.\


**Start fresh**. Create a new generic filament profile.\
&#xNAN;_&#x42;rands update their recipes so the PLA you buy right now from X might not be the same as the "same" ones you bought 3 years ago._

***

### Temperature

First things first: find the ideal temperature in the "normal" range given by the manufacturer.

Look for overhangs first, then bridges and finally overall surface quality.

Once you found the proper temperature:

* [ ] Update the filament profile accordingly.\
  `First Layer Temp = Ideal Temperature + 5°C`
* [ ] Save your profile & quit the project.

***

### Flow Rate

* [ ] Run the **YOLO** test included in Orca Slicer (2.2.0+).
* [ ] Update your filament profile accordingly.

_Proceed again if you're really picky and think quality might get even better._\
_I'd side with Goodenov._

***

### Pressure Advance



***

### Retraction

_Cause ain't nobody wanna see spidey webs on their prints._

***

### Max Volumetric Speed

_This allows you to find how much your printer can actually go Brrrrrrrrrrrrrrrrrrrrrrrrrrrr_



