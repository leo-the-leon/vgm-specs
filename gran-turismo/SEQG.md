Gran Turismo 1-3 SEQG Notes
===========================
Gran Turismo 1, 2, 2000, 3 and Concept use SEQG as their sequence format, with a .SEQ extension.

Format
------

Despite the extension being .SEQ, it doesn't have much to do with Sony's standard .SEQ (SEQp) format. There are lots of differences between the two:
- SEQp is singletrack (like SMF type 0,) SEQG is multitrack with a global tempo value (like SMF type 1)
- SEQp makes actual sense, SEQG is made by PD

GT3/C's version of SEQG has multiple sequences in one file, similar to Sony's .SEP format. Otherwise, the sequence format is untouched.

Header
------

WARNING: Some speculation here

|Offset|Length|Description                                    |
|------|------|-----------------------------------------------|
|  0x00|     4|Identifier (SEQG)                              |
|  0x08|      |Breaks stuff, or something                     |
|  0x0D|     1|Global volume (40 is used, doesn't work in GT1)|
|  0x10|     3|Tempo value (PPQN?)                            |
|  0x13|     N|Offset lists? NRPN stuff?                      |

Sequence
--------

WARNING: Some speculation here too

The sequence data always starts at 0x54, with an 01 02 00 00 sequence marking the end of each track.

There aren't any note-on events(?) unike standard SEQ, notes and time are just stored in pairs, with the delta time first and then succeeded by the note value. Functionally, they're 7bit values in a single byte, with the sign(?) indicating which type of value it is:

|Value|Description|
|-----|-----------|
|00-7F|Delta time |
|80-FF|Note       |

The delta time is variable length, as having two time values next to each other results in a 14bit value.

There are also MIDI messages, which in GT1/2/2K SEQs are usually found at the beginning of each track. They are 3 bytes long, starting with 00 and then followed by status and 7bit (0-127) data bytes. The available status are:

|Status|Description    |
|------|---------------|
|03    |Program Change |
|04    |Volume         |
|05    |Panning        |
|06    |Tempo          |
