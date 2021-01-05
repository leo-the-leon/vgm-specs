OPTION Tuning Car Battle .SHB Notes
===================================
Both OPTION Tuning Car Battle 2 and Spec-R store sequenced music in .SHB files, which can be found rather easily in the SE folder.

Format
------

.SHB files store generic SEQ/VH/VB pairs, with a 12-byte header containing absolute offsets.

|Offset|Length|Description                                                      |
|------|------|-----------------------------------------------------------------|
|  0x00|     4|Offset to SEQ (identifier included, redundant as all are at 0x0C)|
|  0x04|     4|Offset to VH (identifier included)                               |
|  0x08|     4|Offset to VB (16 bytes before start of wave data)                |
