---
layout: default
title: Beacon Format
parent: Bluetooth Beacons
grand_parent: Research
---

Beacons emitted and consumed by droids use data stored in the "Manufacturer Specific Data" section of a Bluetooth beacon. 						
The manufacturer ID will be ``0x0183``, which is Disney's ID number.						
The data can contain one or more sub-sections. Each subsection will begin with two bytes: the first byte specified the type of data, the second byte specifies the length. The data for this subsection then follows.						

For example, a beacon that a droid emits to identify itself has a manufacturer's data value of: ``0x030444818201``	

Breaking this down:	

| Byte        | Description                           |
|-------------|---------------------------------------|
| 03          | the type of data (a droid identifier) |
| 04          | the length of the data                |
| 44 81 82 01 | the data                              |
						
The droid identifier data can be broken down further as:

| Byte | Description                                               |
|------|-----------------------------------------------------------|
| 44   | 0x40 + number of bytes of data including this byte        |
| 81   | 0x01 + (if the droid is paired with a remote: 0x80)       |
| 82   | a combination of the personality chip and its affiliation |
| 01   | the id of the personality chip installed                  |
						
Location beacons can also be decoded in this way. For example: ``0x0A040102A601``		

| Byte | Description                        |
|------|------------------------------------|
| 0A   | the type of data (location beacon) |
| 04   | the length of data                 |
| 01   | 02 A6 01	the data                |
						
Location beacon data breakdown:			

| Byte | Description                                                                                                                                                                                                                                        |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 01   | the location id                                                                                                                                                                                                                                    |
| 02   | minimum interval between droid reactions to the beacon; value multiplied by 5 = number of seconds between reactions; minimum reaction time is 1 minute. This means values less than 0x0C will all result in a 1 minute interval between reactions. |
| A6   | expected Received Signal Strength Indicator (RSSI) in dBm; if weaker then beacon is ignored; 0xA6 would be -38dBm, 0xBA would be -58dBm; a value of about -28dBm is the "highest" usable value (about 1 foot from droid).                          |
| 01   | uncertain; a value of 0 or 1 otherwise the beacon is ignored                                                                                                                                                                                       |