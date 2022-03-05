						
Emulating Beacons						
There are many ways to emulate bluetooth beacons. One of the more accessible ways is to use a bluetooth enabled phone and an app.						
I have found nRF Connect for Android devices works well. This video by VProFX demonstrates using nRF Connect						
	https://www.youtube.com/watch?v=liKQ0LrN9q0					
There is an iOS version of nRF Connect, however it does not allow for simulating beacons.						
You could also use dedicated hardware, such as a BBC Micro:bit as demonstrated by the Burbank Makerspace in this YouTube video: 						
	https://www.youtube.com/watch?v=lnBzoScwhm0					
						
						
	pxt-swge-beacon					
	a MakeCode extension for the micro:bit					
	Allows the micro:bit to emulate droid and location beacons.					
	demonstration					
	what is a micro:bit?					
						
						
Astromech Droid Beacons						
Astromech Droids built at Droid Depot emit a bluetooth beacon while it is active that takes the following format:						
						
	Company ID:	0x0183		yy = affiliation		
	Data:	0x03044481yyzz		zz = personality chip		
						
	Personality Chip	Affiliation	yy Value	zz Value		
	None (R Series)		82	01		
	None (BB Series)		82	02		
	Blue	Resistance	8A	03		
	Gray	Scoundrel	82	04		
	Red	First Order	92	05		
	Orange	Resistance	8A	06		
	Purple	Scoundrel	82	07		
	Black	First Order	92	08		
						
Bluetooth Beacons that Droids React To						
Droids react to the environment based on Bluetooth beacons they encounter.						
Droids emit their own beacon which changes based on the installed personality chip. Other droids will react to those beacons.						
There are also fixed beacons located throughout the park that droids will react to.						
The beacon data, specifically the third byte of the beacon data, appears to control from which group of sounds a sound will play. 						
This is how personality chips control whether a droid reacts with a friendly or frightened noise. For example, a resistance personality chip may have frightened sounds in group 7 which is associated with First Order locations.						
You can simulate these beacons with your phone using an app such as "nRF Connect" and try them out for yourself.						
						
	Manufacturer ID	Data	Land	Location		Notes
	0x183	0x0A040102A601	DL, WDW	Marketplace, Outdoor Areas		
	0x183	0x0A040202A601	DL, WDW	Behind Droid Depot		
	0x183	0x0A040302A601	DL, WDW	Resistance		
	0x183	0x0A040402A601				Have not seen this beacon in any data I have access to
	0x183	0x0A040502A601	DL, WDW	Droid Depot		
	0x183	0x0A040602A601	WDW	Dok-Ondar's		
	0x183	0x0A040702A601	DL, WDW	First Order		
						
	0x183	0x0A040318BA01	DL	Droid Depot		
	0x183	0x0A040618BA01	WDW	Marketplace		
						
	0x183	0x0A0405FFA601	DL, WDW	In front of Oga's		possibly the droid detector
	0x183	0x0A0407FFA601	WDW	In front of Oga's		
						
Types of Beacons						
Below are different beacon formats that have been seen to cause astromech droids reactions.						
						
	Manufacturer ID	Format	Values	Location(s) Seen		
	0x183	0x0A040n02A601	n = {1,2,3,4,5,6,7}	Everywhere		
	0x183	0x0A040nFFA601	n = {1,2,3,4,5,6,7}	Oga's Cantina		
	0x183	0x0A040n18BA01	n = {1,2,3,4,5,6,7}	Marketplace		
						
Beacon Format						
Beacons emitted and consumed by droids use data stored in the "Manufacturer Specific Data" section of a Bluetooth beacon. 						
The manufacturer ID will be 0x0183, which is Disney's ID number.						
The data can contain one or more sub-sections. Each subsection will begin with two bytes: the first byte specified the type of data, the second byte specifies the length. The data for this subsection then follows.						
For example, a beacon that a droid emits to identify itself has a manufacturer's data value of: 0x030444818201						
Breaking this down:						
	03	the type of data (a droid identifier)				
	04	the length of the data				
	44 81 82 01	the data				
						
The droid identifier data can be broken down further as:						
	44	0x40 + number of bytes of data including this byte				
	81	0x01 + (if the droid is paired with a remote: 0x80)				
	82	a combination of the personality chip and its affiliation				
	01	the id of the personality chip installed				
						
Location beacons can also be decoded in this way. For example: 0x0A040102A601						
	0A	the type of data (location beacon)				
	04	the length of data				
	01 02 A6 01	the data				
						
Location beacon data breakdown:						
	01	the location id				
	02	minimum interval between droid reactions to the beacon; value multiplied by 5 = number of seconds between reactions; minimum reaction time is 1 minute. This means values less than 0x0C will all result in a 1 minute interval between reactions.				
	A6	expected Received Signal Strength Indicator (RSSI) in dBm; if weaker then beacon is ignored; 0xA6 would be -38dBm, 0xBA would be -58dBm; a value of about -28dBm is the "highest" usable value (about 1 foot from droid).				
	01	uncertain; a value of 0 or 1 otherwise the beacon is ignored				
						
The above information comes from Russ on the Galaxy's Edge Discord Server. 						
http://swgediscord.com						
						
Datapad App						
The datapad app utilizes bluetooth beacons heavily to identify locations and items to interact with. 						
Emulating the beacons listed below will allow you to utilize the datapad app as if you were in the park. However some features will not work as they require other beacons not listed here.						
						
	Location		Company ID	Data		
	Galaxy's Edge - Walt Disney World		0x4C	0x0215bc85ceaae2e2435db0499b70d5151c3ba0290026ba		
	Galaxy's Edge - Disneyland		0x4C	0x0215be5202c7401744899cb2d73d62cd529da08e0071c0		
						
Resources						
SWGE Discord Server						
bashNinja in the SWGE Discord server made his bluetooth scan data available in the #makerspace channel.						
this data has been especially valuable.						
						
A map showing the locations of beacons found in the park. Compiled by VProFX						
"http://galaxysedgetech.epizy.com/
"						
						
A spreadsheet of beacons and locations by Cowkitty						
https://docs.google.com/spreadsheets/d/1zIZb7uUxUe7ewypnTGrzrX1FA85U5mn2XtULZbcXqI8/edit#gid=0						
						
Burbank Makerspace video on emulating beacons						
https://www.youtube.com/watch?v=lnBzoScwhm0						