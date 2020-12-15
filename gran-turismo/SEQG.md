Gran Turismo 1-3 SEQG Notes
===========================
Gran Turismo 1, 2, 3 and Concept use SEQG as their sequence format, with a .SEQ extension.

Format
------

Despite the extension being .SEQ, it doesn't have much to do with Sony's standard .SEQ (SEQp) format. There are lots of differences between the two:
- SEQp is singletrack (like SMF type 0,) SEQG is multitrack with a global tempo value (like SMF type 1)
- SEQp makes actual sense, SEQG is made by PD

GT3/C's version of SEQG has multiple sequences in one file, similar to Sony's .SEP format. Otherwise, the sequence format is untouched.

Header:

WARNING: Some speculation here

|Offset|Length|Description                |
|------|------|---------------------------|
|  0x00|     4|Identifier (SEQG)          |
|  0x08|      |Breaks stuff, or something |
|  0x0D|     1|Global volume (GT2 uses 40)|
|  0x10|     3|Tempo value (PPQN?)        |
|  0x13|     N|Offset lists? NRPN stuff?  |

Sequence:

WARNING: Some speculation here too

Each track starts with the 4-byte sequence 00 00 00 03, except for spu_04.seq in GT2, which uses 00 00 78 03 for the first track.

There aren't any note-on events(?) unike standard SEQ, notes and time are just stored in pairs, with the delta time first and then succeeded by the note value. Functionally, they're 7bit values in a single byte, with the sign(?) indicating which type of value it is:

|Value|Description|
|-----|-----------|
|00-7F|Delta time |
|80-FF|Note       |

The delta time is variable length, as having two time values next to each other results in a 14bit value.
