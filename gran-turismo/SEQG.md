Gran Turismo 1-3 SEQG Notes
===========================
Gran Turismo 1, 2, 2000, 3 and Concept use SEQG as their sequence format, with a .SEQ extension.

Format
------

Despite the extension being .SEQ, it doesn't have much to do with Sony's standard .SEQ (SEQp) format. There are lots of differences between the two:
- SEQp is singletrack (like SMF type 0,) SEQG is multitrack with a global tempo value (like SMF type 1)
- SEQp makes actual sense, SEQG is made by PD

GT3/C's version of SEQG has multiple sequences in one file, similar to Sony's .SEP format. Otherwise, the format is similar.

Header
------

WARNING: Some speculation here

For GT1, 2 and 2000:

|Offset|Length|Description                                    |
|------|------|-----------------------------------------------|
|  0x00|     4|Identifier (SEQG)                              |
|  0x04|     4|Offset to start of file                        |
|  0x08|      |Breaks stuff, or something                     |
|  0x0D|     1|Global volume (40 is used, doesn't work in GT1)|
|  0x10|     3|Tempo value (PPQN?)                            |
|  0x14|  4*16|Offset to tracks                               |
|  0x54|     N|Beginning of sequence data                     |

It is important to note that GT1 loads all SEQs at once, while GT2 only loads one. GT1 only overwrites relative (to the file) offsets with absolute ones once the SEQ that has them starts playing.

Sequence
--------

WARNING: Some speculation here too

There aren't any note-on events unike standard SEQ, notes and time are just stored in pairs, with the delta time first and then succeeded by the note value. Functionally, they're 7bit values in a single byte, with the signing bit indicating which type of value it is:

|Value|Description                        |
|-----|-----------------------------------|
|00-7F|Delta time, velocity, note duration|
|80-FF|Note                               |

The delta time is variable length, as having two time values next to each other results in a 14bit value.

The note value can also be succeeded by a velocity value, and then after that a note duration.

There are also events, which in GT1/2/2K SEQs are usually found at the beginning of each track. They are 3 bytes long, starting with 00 and then followed by type and 7bit (0-127) value bytes. The available types are:

|Type|Description    |Notes                                |
|----|---------------|-------------------------------------|
|01  |Loop marker    |First marker value is number of loops|
|02  |End of track   |                                     |
|03  |Program Change |Starts from 01(?)                    |
|04  |Volume         |                                     |
|05  |Panning        |                                     |
|06  |Tempo          |I don't think this is used           |
