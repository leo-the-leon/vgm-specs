OPTION Tuning Car Battle .SHB Notes
===================================
Both OPTION Tuning Car Battle 2 and Spec-R store sequenced music in .SHB files, which can be found rather easily in the SE folder.

Format
------

.SHB files store generic SEQ/VH/VB pairs, with a 12-byte header containing offsets relative to the very start of the file (aka including the header.)

|Offset|Length|Description                                                      |
|------|------|-----------------------------------------------------------------|
|  0x00|     4|Offset to SEQ (identifier included, redundant as all are at 0x0C)|
|  0x04|     4|Offset to VH (identifier excluded)                               |
|  0x08|     4|Offset to VB (8 bytes before start of wave data)                 |
