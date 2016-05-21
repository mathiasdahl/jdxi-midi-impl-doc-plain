      
# MIDI Implementation

<pre>
Model:   JD-Xi
Date:    May 1, 2015
Version: 1.00
</pre>

## 1. Data Reception (Sound Source Section)

### Channel Voice Messages

#### Note off

<pre>
Status  2nd byte 3rd byte
------  -------- --------
8nH     kkH      vvH
9nH     kkH      00H

n  = MIDI channel number:  0H  - FH  (ch.1 - 16)
kk = note number:          00H - 7FH (0 - 127)
vv = note off velocity:    00H - 7FH (0 - 127)
</pre>

### Note on

<pre>
Status  2nd byte 3rd byte
------  -------- --------
9nH     kkH      vvH

n = MIDI channel number:  0H  - FH  (ch.1 - 16)
kk = note number:         00H - 7FH (0 - 127)
vv = note on velocity:    01H - 7FH (1 - 127)
</pre>

### Polyphonic Key Pressure

<pre>
Status  2nd byte 3rd byte
------  -------- --------
AnH     kkH      vvH

n = MIDI channel number:      0H - FH (ch.1 - 16)
kk = note number:             00H - 7FH (0 - 127)
vv = Polyphonic Key Pressure: 00H - 7FH (0 - 127)

(*) Not received when the Receive Polyphonic Key Pressure parameter (SysEx) is OFF.
</pre>

### Control Change

#### Bank Select (Controller number 0, 32)

<pre>
Status  2nd byte 3rd byte
------  -------- --------
BnH     00H      mmH
BnH     20H      llH

n = MIDI channel number:  0H - FH (ch.1 - 16)
mm, ll = Bank number:     00 00H - 7F 7FH (bank.1 - bank.16384)

(*) Not received when the Receive Bank Select parameter (SysEx) is OFF.
</pre>

The Programs corresponding to each Bank Select are as follows.

<pre>
BANK SELECT      | PROGRAM   | GROUP                      | NUMBER
MSB  | LSB       | NUMBER    |                            |
-----+-----------+-----------+----------------------------+-----------
085  | 000       | 001 - 064 | User Bank Program (E)      | E01 - E64
085  | 000       | 065 - 128 | User Bank Program (F)      | F01 - F64
085  | 001       | 001 - 064 | User Bank Program (G)      | G01 - G64
085  | 001       | 065 - 128 | User Bank Program (H)      | H01 - H64
-----+-----------+-----------+----------------------------+-----------
085  | 064       | 001 - 064 | Preset Bank Program (A)    | A01 - A64
085  | 064       | 065 - 128 | Preset Bank Program (B)    | B01 - B64
085  | 065       | 001 - 064 | Preset Bank Program (C)    | C01 - C64
085  | 065       | 065 - 128 | Preset Bank Program (D)    | D01 - D64
-----+-----------+-----------+----------------------------+-----------
085  | 096       | 001 - 064 | Extra Bank Program (S)     | S01 - S64
     | :         | :         | :                          | :
085  | 103       | 001 - 064 | Extra Bank Program (Z)     | Z01 - Z64
</pre>
