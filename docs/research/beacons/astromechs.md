---
layout: default
title: Astromechs
parent: Bluetooth Beacons
grand_parent: Research
---

# Astromech Droid Beacons						

Astromech Droids built at Droid Depot emit a bluetooth beacon while it is active that takes the following format:						

```						
 Company ID: 0x0183
 Data: 0x03044481yyzz		
```

 | Field | Description      |
 |-------|------------------|
 | yy    | affiliation      |
 | zz    | personality chip |

 | Personality Chip 	| Affiliation | yy Value | zz Value |
 |----------------------|-------------|----------|----------|
 | None (R Series)  	| 82          | 01       |          |
 | None (BB Series) 	| 82          | 02       |          |
 | Blue	Resistance   	| 8A          | 03       |          |
 | Gray	Scoundrel    	| 82          | 04       |          |
 | Red	First Order   	| 92          | 05       |          |
 | Orange	Resistance 	| 8A          | 06       |          |
 | Purple	Scoundrel  	| 82          | 07       |          |
 | Black	First Order | 92          | 08       |          |

# Bluetooth Beacons that Droids React To						

Droids react to the environment based on Bluetooth beacons they encounter.						
Droids emit their own beacon which changes based on the installed personality chip. Other droids will react to those beacons.						
There are also fixed beacons located throughout the park that droids will react to.						
The beacon data, specifically the third byte of the beacon data, appears to control from which group of sounds a sound will play. 						
This is how personality chips control whether a droid reacts with a friendly or frightened noise. For example, a resistance personality chip may have frightened sounds in group 7 which is associated with First Order locations.						
You can simulate these beacons with your phone using an app such as "nRF Connect" and try them out for yourself.						
						
 | Manufacturer ID | Data           | Land    | Location                                               | Notes                       |
 |-----------------|----------------|---------|--------------------------------------------------------|-----------------------------|
 | 0x183           | 0x0A040102A601 | DL, WDW | Marketplace, Outdoor Areas                             |                             |
 | 0x183           | 0x0A040202A601 | DL, WDW | Behind Droid Depot                                     |                             |
 | 0x183           | 0x0A040302A601 | DL, WDW | Resistance                                             |                             |
 | 0x183           | 0x0A040318BA01 | DL      | Droid Depot                                            |                             |
 | 0x183           | 0x0A040402A601 |         | Have not seen this beacon in any data I have access to |                             |
 | 0x183           | 0x0A040502A601 | DL, WDW | Droid Depot                                            |                             |
 | 0x183           | 0x0A0405FFA601 | DL, WDW | In front of Oga's                                      | Possibly the droid detector |
 | 0x183           | 0x0A040602A601 | WDW     | Dok-Ondar's                                            |                             |
 | 0x183           | 0x0A040618BA01 | WDW     | Marketplace                                            |                             |
 | 0x183           | 0x0A040702A601 | DL, WDW | First Order                                            |                             |
 | 0x183           | 0x0A0407FFA601 | WDW     | In front of Oga's                                      |                             |
						
# Types of Beacons						

Below are different beacon formats that have been seen to cause astromech droids reactions.						
						
| Manufacturer ID | Format         | Values              | Location(s) Seen |
|-----------------|----------------|---------------------|------------------|
| 0x183           | 0x0A040n02A601 | n = {1,2,3,4,5,6,7} | Everywhere       |
| 0x183           | 0x0A040nFFA601 | n = {1,2,3,4,5,6,7} | Oga's Cantina    |
| 0x183           | 0x0A040n18BA01 | n = {1,2,3,4,5,6,7} | Marketplace      |