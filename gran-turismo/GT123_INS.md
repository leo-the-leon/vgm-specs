Gran Turismo 1-3 .INS Notes
===========================
Gran Turismo 1, 2, 3 and Concept use .INS as their sample bank format. 

Format
------

.INS is a modified variant of Sony's VAB format, and thus is quite similar to it, but the VH part is nonstandard and thus will not work properly with tools like VABTool or Awave Studio.

WARNING: GT2 was used for testing here, might not apply to other games

Header:

|Offset|Length|Description                     |Notes                                                                     |
|------|------|--------------------------------|--------------------------------------------------------------------------|
|  0x00|     4|Identifier (INST)               |                                                                          |
|  0x04|     4|Pointer to start of file        |Converted to absolute offset at runtime                                   |
|  0x08|     4|Size of header                  |                                                                          |
|  0x0C|     4|???                             |Converted to something at runtime (0x00000000 to 0x10100000 with sys.ins) |
|  0x14|     4|Pointer to start of sample data |Same as 0x08 but is converted to absolute offset at runtime               |

Instruments:

|Offset|Length|Description       |Notes                                                       |
|------|------|------------------|------------------------------------------------------------|
|  0x00|     2|Pointer to sample |Multiple of 0x08, must be even                              |
|  0x02|     2|Sample volume     |0x0B87-0x8888 give phase-cancelled stereo sound             |
|  0x04|     2|Reverse frequency |Might be SPU period value                                   |
|  0x06|     2|Length            |Could be either sample or envelope length                   |
|  0x08|     2|???               |Always 0x0040                                               |
|  0x0A|     2|Reverb toggle     |0x0100 enables reverb                                       |
|  0x0C|   1x2|MIDI center pitch |Paired with a duplicate, which is ignored in retail GT1/GT2 |
|  0x0E|     2|???               |Always 0x0000                                               |
|  0x10|     2|Attack env. node  |Signed, larger value = longer fade from 0 to max volume     |
|  0x12|     2|Release env. node |Signed, larger value = longer fade from max volume to 0     |
