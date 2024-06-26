## SysEx dumps

The ultimate goal is to create an open source configuration tool, but one may already use these SysEx commands to change the basic controller mode, e.g. using `aseqsend`:

```
~$ aseqsend -l
 Port    Client name                      Port name
 40:0    SINCO                            SINCO MIDI 1
129:0    FootCtrl                         FootCtrl Bluetooth
~$ aseqsend -p 40:0 "F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 0B 5E 03 F7" # switch to "Program change C" mode
~$ aseqsend -p 40:0 "F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 06 68 03 F7" # switch to "Manufacturer control" mode
```

(SysEx over BLE MIDI towards `129:0` didn't seem to work, maybe the commands are different)

### General messages

"OK" response: sysex sent by the controller after each configuration change

```
F0 00 32 01 08 00 00 00 00 7F 01 F7
```

### Discovery

Request:

```
F0 00 32 45 00 00 00 40 7F F7
```

Response:

```
F0 00 32 45 58 01 00 00 23 6F 5E 51 1B 44 4E 1C 36 5F 60 4C 09 03 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 60 37 F7
```

### Connecting and requesting current settings

(TODO: screenshot of the resulting settings)

Request:

```
F0 00 32 0D 41 00 00 00 02 00 00 00 00 10 7E 00 00 07 00 F7
F0 00 32 0D 41 00 00 00 02 71 07 00 00 10 6A 00 00 33 01 F7
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 20 30 03 F7
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 21 2A 03 F7
F0 00 32 09 49 00 00 00 02 06 00 00 00 10 00 00 00 22 24 03 F7
F0 00 32 09 49 00 00 00 02 08 00 00 00 10 00 00 00 03 5E 03 F7
F0 00 32 09 49 00 00 00 02 0A 00 00 00 10 00 00 00 2C 08 03 F7
F0 00 32 09 49 00 00 00 02 32 0E 00 00 10 00 00 00 07 74 02 F7
F0 00 32 09 49 00 00 00 02 36 0E 00 00 10 00 00 00 09 68 02 F7
F0 00 32 09 49 00 00 00 02 3A 0E 00 00 10 00 00 00 0A 5E 02 F7
F0 00 32 09 49 00 00 00 02 3E 0E 00 00 10 00 00 00 0B 54 02 F7
```

Response:

```
F0 00 32 0D 49 3F 00 00 02 00 00 00 00 10 7E 00 00 01 00 00 09 10 24 00 11 01 06 04 60 02 20 00 00 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 01 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 01 00 00 78 07 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 08 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 4C 03 F7
F0 00 32 0D 49 35 00 00 02 71 07 00 00 10 6A 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 07 00 00 00 10 01 00 00 00 14 00 00 00 60 02 00 00 00 38 04 F7
[9 x OK]
```

### TRS = Expression Pedal

```
F0 00 32 09 49 00 00 00 02 0C 00 00 00 10 00 00 00 00 5C 03 F7
```

### TRS = MIDI

```
F0 00 32 09 49 00 00 00 02 0C 00 00 00 10 00 00 00 01 5A 03 F7
```

### Program change A

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 00 74 03 F7
```

### Program change B

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 01 72 03 F7
```

### Program change C

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 0B 5E 03 F7
```

### Touch screen (Android)

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 02 70 03 F7
```

### Keyboard A

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 03 6E 03 F7
```

### Keyboard B

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 04 6C 03 F7
```

### MultiMedia keyboard

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 05 6A 03 F7
```

### Manufacturer control

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 06 68 03 F7
```

### Custom mode

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 07 66 03 F7
```

#### A

Momentary (aka "Visual Behavior Off"):

```
F0 00 32 09 49 00 00 00 02 03 00 00 00 10 00 00 00 00 6E 03 F7
```

Latching (aka "Visual Behavior On"):

```
F0 00 32 09 49 00 00 00 02 03 00 00 00 10 00 00 00 01 6C 03 F7
```

Set CC = 0, 1, 2, 3, ..., 125, 126, 127:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 00 70 03 F7
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 01 6E 03 F7
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 02 6C 03 F7
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 03 6A 03 F7
[...]
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 7D 76 01 F7
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 7E 74 01 F7
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 7F 72 01 F7
```

Channel Aftertouch:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 00 71 01 F7
```

Start:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 01 6F 01 F7
```

Stop:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 02 6D 01 F7
```

Continue:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 03 6B 01 F7
```

Active Sensing:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 04 69 01 F7
```

Reset:

```
F0 00 32 09 49 00 00 00 02 02 00 00 00 10 00 00 00 05 67 01 F7
```

#### B

Momentary:

```
F0 00 32 09 49 00 00 00 02 05 00 00 00 10 00 00 00 00 6A 03 F7
```

Latching:

```
F0 00 32 09 49 00 00 00 02 05 00 00 00 10 00 00 00 01 68 03 F7
```

Set CC = 0, 1, 2, 3, ..., 125, 126, 127:

```
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 00 6C 03 F7
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 01 6A 03 F7
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 02 68 03 F7
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 03 66 03 F7
[...]
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 7D 72 01 F7
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 7E 70 01 F7
F0 00 32 09 49 00 00 00 02 04 00 00 00 10 00 00 00 7F 6E 01 F7
```

(TODO)

#### C

TODO

#### D

TODO

#### Expression Pedal

TODO

### Video Mode

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 08 64 03 F7
```

### Advanced custom mode

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 09 62 03 F7
```

TODO

### Custom keyboard mode

```
F0 00 32 09 49 00 00 00 02 00 00 00 00 10 00 00 00 0A 60 03 F7
```

TODO
