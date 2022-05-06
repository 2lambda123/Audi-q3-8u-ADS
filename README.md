# Audi Q3 (8U) AudiDriveSelect (ADS) activation
Enabling AudiDriveSelect in Audi Q3 (8U).

![Audi RMC with AudiDriveSelect screen option](https://github.com/mrfixpl/Audi-q3-8u-ADS/blob/main/images/RMC-AudiDriveSelect.jpg?raw=true)

## What is ADS?
ADS is short for Audi Drive Select. It allows the driver to choose from different driving modes: comfort, normal, auto, dynamic, efficiency, individual. Depending on installed options, there are settings for engine, gearbox, suspension, exhaust, cornering lights.

## Tools required

## Procedure
### Gateway
* Parameterization required. Can be done with VCP or ODIS.
* Module `0x19`, address `0x1200`, upload dataset:
  * `datasets/19-gateway/0x1200_ADS-withoutEfficiency` - with ADS (comfort, auto, dynamic)
  * `datasets/19-gateway/0x1200_ADS-withEfficiency` - with ADS (comfort, auto, dynamic, efficiency)
  * `datasets/19-gateway/0x1200_noADS` - no AudiDriveSelect

### Infotainment
#### Audi `RMC2`
* Parameterization required. Can be done with VCP, ODIS, OBDeleven.
* Module `0x5F`, address `0xF00610`, upload dataset:
  * `datasets/5f-rmc2/0xF00610_CarMenu-withADS` - with AudiDriveSelect menu
  * `datasets/5f-rmc2/0xF00610_CarMenu-withoutADS` - without AudiDriveSelect menu
* Check this for more details: https://github.com/mrfixpl/audi-rmc-coding-adaptation-datasets
* Parameterization with OBDeleven: https://www.youtube.com/watch?v=jsi80Yr3aoY

#### Audi `RMC4`
* Parameterization required. Can be done with VCP, ODIS, OBDeleven.
* Module `0x5F`, address `0xF00710`, upload dataset:
  * `datasets/5f-rmc4/0xF00710_CarMenu-withADS` - with AudiDriveSelect menu
  * `datasets/5f-rmc4/0xF00710_CarMenu-withoutADS` - without AudiDriveSelect menu
* Check this for more details: https://github.com/mrfixpl/audi-rmc-coding-adaptation-datasets
* Parameterization with OBDeleven: https://www.youtube.com/watch?v=jsi80Yr3aoY

#### Audi MMI 3G+ (`HN+`)
* Green Engineering Menu access required - need to enable developer mode first
  * Module `0x5F`, adaptation, channel `6`, new value `1`.
  * Reboot unit with button combination: **[BACK]** + **[Control Wheel]** + **[Upper-Right]**
  * Reboot demo: https://youtu.be/KxOsZpEe3cY
* Enable ADS/Charisma
  * Enter GEM with button combination: **[CAR]** + **[MENU]**
  * Go to `car/cardevicelist/carisma` and enable it.
  * Go to `car/carmenuoperation/carisma` and set it to `5`.
  * Reboot unit with button combination: **[BACK]** + **[Control Wheel]** + **[Upper-Right]**

## Research
* Last 4 bytes in gateway dataset is CRC-32 checksum,
* Last 2 bytes in RMC dataset is CRC-16/CCITT-FALSE checksum,
* Modes in order: *Individual*, **Comfort**, **Auto**, **Dynamic**, *Offroad*, **Efficiency**, *Race*.
* Looking at the gateway dataset, it seams that it supports all 7 modes, but *Offroad* and *Race* are not enabled. Might be possible to alter the dataset to get mode modes.
* Individual settings in order: engine/transmission, suspension, steering, 4x4, exhaust, belt tensioner, ACC. Additionally: contour seats, cornering lights.

## Credits, reference, links
* Huge thanks to everyone involved in this research!
* MQB-FPA: https://github.com/jilleb/MQB-FPA/wiki/dataset
* ADS modes in A6 C7: https://www.audizine.com/forum/showthread.php/433578-Compiled-Drive-Select-VAG-COM-codes?p=7823311&viewfull=1#post7823311
* Checksum calculator: https://crccalc.com/
* Parameterization with OBDeleven: https://www.youtube.com/watch?v=jsi80Yr3ao
* OBDeleven diagnostic interface (ref link): http://obdeleven.com/?src=link&ref=Zy245Iacqc6bMTHh
