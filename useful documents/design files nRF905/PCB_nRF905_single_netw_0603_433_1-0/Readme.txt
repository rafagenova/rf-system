This file contains an overview of the NC drill files and Gerber files included in the Zip archive file "PCB_nRF905_single_netw_0603_433_1-0.ZIP".

Read application note nAN900-04 "nRF905 RF and antenna layout" before using the included files.


NC drill files
The Zip archive file contains NC drill files in both Excellon and ASCII format.

nRF905_single_netw_0603_1-0.drr :
Report file. Details the tools used, the hole sizes in both metric and imperial, the number of holes and the tool travel.

nRF905_single_netw_0603_1-0.drl :
Excellon format drill file.

nRF905_single_netw_0603_1-0.txt:
An ASCII version of the Excellon format file with the extension TXT.

The drill control files (Extension DRL) are written in the EIA character (binary) format in the EXCELLON language. The data is specified in mils with trailing zero suppressed. Drill tools are numbered from 1 up to 255.


Gerber files
The Gerber plot file names are appended with a unique extension that
identifies layer and plot type. The Gerber extensions are;

Top Overlay		.GTO
Top Layer		.GTL
Bottom Layer		.GBL
Top Solder Mask	.GTS
Bottom Solder Mask	.GBS
Top Paste Mask		.GTP
Mechanical Layer 1, etc..GM1 (naming of I/O signals and outline info)
Drill Drawing		.GD1
Drill Guide		.GG1

The apertures are written into the Gerber files according to the RS274X Gerber file specification.
