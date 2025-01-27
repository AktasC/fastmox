---
description: >-
  No-nonsense 3D printing calibration guide | Orca Slicer | Bambu Lab - P1S x
  AMS
---

# ⚙️ Calibration

Do these calibrations with the "0.20mm Standard" profile, _stop fµcking around kid_.

## Filament Calibration

{% hint style="warning" %}
**Don't forget to calibrate your printer first.**
{% endhint %}

It's a good idea to make sure your belts are properly tensioned before attempting any calibration process. I know, it's a pain in the ass, but making sure the hardware is properly calibrated first will ensure you get valid, consistant and thus usable calibration results.

As I have a P1S, I'll follow these steps:&#x20;

* [ ] Check belts - retension if necessary
* [ ] Inspect carbon rods & Z-axis linear rods - _Wipe with Isopropanol once a month_
* [ ] Check Z-axis lubrication - _Clean & lubricate if necessary / if you see plastic debris stuck_
* [ ] Run the 30mn calibration process, get a coffee.

{% hint style="success" %}
**Start fresh**. Create a new generic filament profile.\
&#xNAN;_&#x42;rands tend to change their recipes over time, so the PLA you buy right now from vendor X might not be exactly the same as the ones you bought a year ago._
{% endhint %}

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

Run the `Pattern` calibration process, the tower method is harder to gauge and the line method takes as long as the pattern method with less "precision".

Most of the time my ideal value is somewhere around `0.015`.\
You can make an initial broader pass with a startValue of 0, maxValue of 0.4 and a stepValue of 0.05.\
Then you can make a second pass with startValue and maxValue set according to your first results and a finer stepvalue of 0.01 or 0.005 if you're REALLY into torturing your eyes and mind.

To find the your filament's ideal P.A value:

1. Find the line with the smallest value where the tip is sharp but slightly raised
2. Find the line with the highest value, but below the previous value, where the tip is rounded
3. Your ideal value is somewhere between those two\
   I'd even go as far as to say it probably is the one 2 steps below the line you found in the first step.

Note your value, quit the project, discard the changes, open a new project, update your filament profile with said value.\
&#xNAN;_&#x53;ave it. Twice. Just to make sure._

***

### Max Volumetric Speed

{% hint style="info" %}
_This allows you to find how much your printer can actually go Brrrrrrrrrrrrrrrrrrrrrrrrrrrr_
{% endhint %}

You need to understand that setting print speed to 300mm.s won't change anything if your filament's max flowrate is set at 15mm^3.s; that's why we need to find how fast it can go before going Brrrrrrrrr.

Most PLA & PETG can be printed at around 15-20mm3/s with no issues on the P1S.\
&#xNAN;_(That being said, I've installed a CHT nozzle on mine and reached a clean 28mm3/s on most PLA)_

Run the calibration process with a `startValue` at 10 or 15, a `maxValue` of 35 and a `stepValue` of 0.5 .

Look at the print from different angles and:&#x20;

* Find where the sheen changes.\
  &#xNAN;_&#x54;his might be accompanied or preceded by artefacts  or inconsistencies._
* Find the point where inconsistencies start and measure its height in mm.

Use the following calculation to determine the correct max flow value to save:

`startValue + ( {measuredHeight in mm} * stepValue) - 1`

***

### Retraction (optional)

{% hint style="info" %}
_Cause ain't nobody wanna see spidey webs on their prints, right ?_
{% endhint %}

This one is pretty self explanatory so ...\
`startValue:` _0mm_\
`maxValue`_: 1mm_\
`steps`_: 0.1mm_

Look for the height where there are no strings and no blobs visible.\
_Don't forget to update your filament profile with the result value._
