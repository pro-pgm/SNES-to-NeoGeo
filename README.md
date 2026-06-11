SNES to Neo Geo / JAMMA DB15
============================

This is an Arduino project which allows you to interface a SNES or Super Famicom controller
(or a clone) to a Neo Geo style DB15 connector. This version is adapted for
6-button supergun or DIY supergun setups, while still supporting the standard
4-button Neo Geo layout.

I created this for my CMVS project (consolizing a MVS Neo Geo arcade motherboard), and I had
some nice, working SNES controllers that I wanted to use. SNES controllers are quite a good fit
for the Neo Geo because the button colours match (well, except on the purple USA ones!).

It looked easy enough to rewire the controllers and attach a new socket, but I wanted something
that left them in their original state so I could still use them on my SNES.

![Image](ProMini.jpg?raw=true)

This shows a completed project on a cheap Arduino Pro Mini (5v) clone wired up to a SNES female
socket and female DB15 for easy connections. The current 6-button sketch has been tested on an Arduino Nano.

SNES female controller sockets are available on eBay for a couple of pounds, and a Pro Mini
clone costs about the same, so the total cost of the project is only about five pounds.

SNES Controller -> Arduino
--------------------------

```
  -----------------\
  | 1 2 3 4 | 5 6 7 |
  -----------------/
  
  Pin 1: +5V
  Pin 2: Clock -> Arduino A0
  Pin 3: Latch -> Arduino A1
  Pin 4: Serial -> Arduino A2
  Pin 7: GND
```

Arduino -> JAMMA / DB15
-----------------------

```
    1(=GND)        8(=5V)
  \-------------------/
   \ o o o o o o o o / [Viewed from front]
    \ o o o o o o o /
     --------------- 
      9          15

 JAMMA 1P     JAMMA 2P     DB15 Pin  ->  Arduino
 --------     --------     --------      -------
 1 (GND)      1 (GND)      1 (GND)       GND
 3 (+5V)      3 (+5V)      8 (+5V)       +5V
 16 (Credit)  T (Credit)   3 (Sel)       D2
 17 (Start)   U (Start)    11 (Start)    D3
 18 (Up)      V (Up)       15 (Up)       D4
 19 (Down)    W (Down)     7 (Down)      D5
 20 (Left)    X (Left)     14 (Left)     D6
 21 (Right)   Y (Right)    6 (Right)     D7
 22 (A)       Z (A)        13 (A)        D8
 23 (B)       AA (B)       5 (B)         D9
 24 (C)       AB (C)       12 (C)        D10
 25 (D)       AC (D)       4 (D)         D11
 26 (E)       AD (E)       10 (E)        D12
 27 (F)       AE (F)       2 (F)         D17 / A3 on Arduino Nano
```

The sketch maps the SNES buttons as follows:

```
SNES B      -> DB15 B
SNES Y      -> DB15 C
SNES Select -> DB15 Select / JAMMA Credit
SNES Start  -> DB15 Start / JAMMA Start
SNES D-pad  -> DB15 directions
SNES A      -> DB15 A
SNES X      -> DB15 D
SNES L      -> DB15 E
SNES R      -> DB15 F
```

For 8BitDo SNES receivers, the sketch can also mirror SNES L to Start so a long-press reset
shortcut still works.

3d printed case
---------------

I've designed a simple box for the device that can be 3d printed. It fits the Pro Mini inside
along with the SNES socket and a cable grip for a DB15 cable.

The case is designed to fit a cable grip extracted from a UK mains plug (with 16mm spacing between
the grip screws).

The STL files are included here along with the source SCAD files if you need to make any tweaks to
the design.

![Image](3dPrint.jpg?raw=true)

![Image](3dPrint2.jpg?raw=true)

