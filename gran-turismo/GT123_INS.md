Gran Turismo 1-3 .INS Notes
===========================
Gran Turismo 1, 2, 3 and Concept use .INS as their sample bank format. 

Format
------

.INS is a modified variant of Sony's VAB format, and thus is quite similar to it, but the VH part is nonstandard and thus will not work properly with tools like VABTool or Awave Studio.

Header:

|Offset|Length|Description                  |
|------|------|-----------------------------|
|  0x00|     4|Identifier (INST)            |
|  0x04|     4|Offset to start of file (0x0)|
|  0x08|     4|Offset to end of parameters  |
|  0x14|     4|Offset to end of parameters  |
|  0x28|     4|Start of parameters          |

Instruments (TO-DO: rearrange these in the correct order):

|Offset|Length|Type   |Description                               |
|------|------|-------|------------------------------------------|
|  0x00|     2|       |Start of instrument parameters? (00 40)   |
|  0x02|     1|boolean|Enable/disable reverb                     |
|  0x03|     1|       |??? (always 00)                           |
|  0x04|     1|int    |MIDI center pitch (7bit, 80-FF are broken)|
|  0x05|     1|int    |MIDI center pitch? (left/right setup?)    |
|  0x06|     2|       |??? (always 00 00)                        |
|  0x08|     2|uint   |Attack node                               |
|  0x0A|     2|uint   |Release node                              |
|  0x0C|     N|       |Sample offsets?                           |        
|  0x??|     1|       |Instrument volume                         |
|  0x??|     1|uint   |MIDI center pitch (8bit, inverted)        |
