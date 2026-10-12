# Simple circuit simulation with NGSPICE

## About

The goal of this project was to design a very simple audio circuit in KiCad
and then simulate its functionality using NGSPICE. Because I don't do this
type of work that often, a secondary goal was to document the process so
that I can remember how do it later.

The circuit uses a simple inverting op-amp buffer stage with a gain of 2.
The selected op-amp is an NE5524. (The model file for this is also in this
repo, under the part-models directory.) I used the NE5524TI_SN model.

## Key Points

1. To run correctly, the simulation of course requires a power source. In
my circuit. Off to the left of the schematic, you'll see two DC power 
sources: V1 and V2. Note that they are both 17v, and they are tied together
to a 0v ground reference. These symbols came from the Simulation_SPICE
symbol category. 

The +17V rail is tied to a + power pin (+17v) and the -17v rail is tied
to a - power pin.  The actual voltages are dictated by the value on V1,V2.

3. V3 is the source of the signal for the simulation.  You will want to 
choose this from the Simulation_SPICE category of symbols as well. Edit the
Simulation Model parameters acccordingly. Settin the AC magnitude to 1 is
good because it will make the gain chart make sense (e.g. the gain of 2x
will show ~6dB of gain.) The other side of V3 must be grounded to the 0v
reference.

4. The NE5524 IC symbol has to be edited to set the simulation model. I
chose the TI model for that part in library included in this repo. The
most **important** thing to remember for this is that you will likely
need to edit the pin assignments for the part.

Double-click the symbol to launch the "Symbol Properties" dialog. Then
click the **Simulation Model** button.  That should bring up the
**Simulation Model Editor** dialog box. The assignments I used for the
TI model were:

| Symbol Pin | Model Pin | Comment |
| --- | --- | --- |
| 1 | N.C. | - |
| 2 | 2 | Inverting input |
| 3 | 1 | Non-inverting input |
| 4 | 4 | Negative power supply |
| 5 | N.C. | - |
| 6 | 5 | Output |
| 7 | 3 | Positive power supply |
| 8 | N.C. | - |

5. My schematic has two test points TP1, TP2. These are both excluded
from the simulation. To do this, double-click on the symbol and click
the checkbox that says "exclude from simulation." If you don't exclude
them, the electrical rule check will complain.

6. Add labels (Press 'L' in KiCad) to label nets in the diagram. In my
schematic, I have two labeled "in" and "out". These both can be selected
in the simulation dialog so that I can see the input signal and output
signal plotted.

## Extra Notes
The KiCad project in this repo was made with KiCad 9.0.2 for Linux.

