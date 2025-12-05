# TachoPulser
Hardware for driving OEM coil based tachometers.  Simple circuit using a 2N5551 - a high-voltage NPN transistor to drive a DR125-124 inductor to create a high-voltage 'pulse' that triggers OEM tachometers.  

![TachoPulser Board](/BoardOverview.png)

### Purchase
If you want to purchase an assembled TachoPulser, you can do so here: [MK1 & MK2 Golf Coil Tacho RPM Converter - Forbes Automotive](https://forbes-automotive.com/products/ecu-to-coil-tacho-adapter)

## Installation
Boards are supplied with 1x 4-pin JST-XH cable with the connections marked on the board.

### Wiring
> ECU - trigger wire from the ECU

> CLOCKS - the high-voltage pulse to the cluster

> GND - chassis ground

> PWR - 12v ignition power

## Circuit Design
Traditional ignition coils create a high-voltage 'spike' when the current is removed.  The concept of this circuit is to re-create this by charging and collapsing the 'ignition coil'.  A "DR125-124-R" inductor is used as this shares a similar 'resistance' and very low inductance value which mimicks an OEM ignition coil.

The specification for the DR125-124 has a resistance value of 150ohms.  At 12v, this will draw ~0.08A, so the schematic rounds this to 0.1A with a factor of 10 to ensure the base of the transistor is driven hard enough.  The 2N5551 is a high-voltage transistor capable of 600mA (0.6A).

Therefore; the current into the base is: 
Ib = (0.1A x Overdrive Factor) / Beta
Ib = (0.1A x 10) / 30 (min)
Ib = 0.033A

Solving for the resistance value to limit current into the base:
Rb = (Vcc-Transistor Loss) / Ib
Rb = (12.0-0.7) / 0.033
Rb = 330ohm

At 1k, 0.1A can pass (zero ODF).

The RPM is then converted into a lower frequency pulse (ranging typically from 0 to 230hz).  
![TachoPulser Schematic](/Schematic.png)
