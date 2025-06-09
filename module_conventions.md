# Module Design Guidlines

Aquarius's system architecture is based on modules, making it flexible and expandable. This, however, comes with a few down sides. Predominately, it creates additional complexity in the mechanical design. As such, we have established a few broad guideline to assist in the development of new modules.

## General
---
All Aquarius modules:

1. must follow PCB and Schematic guidelines
1. should be as close to 50x50mm as possible.
1. may operate at 3.3v or 5v.
1. requiring power values other than 3.3v and 5v must provide their own
1. inputs and output must be 3.3v ONLY
1. must have two power connectors to allow daisy chaining, JST SH 4
1. must only receive power from the power connector
1. must have at least one QWICC connector, JST SH 4, for communication
1. with programmable MCU must use 6 pin, 2x3, 2.54mm spacing, for programming
1. must have at least 2, with 4 perferable, mounting holes.
1. mounting holes must be 3.2mm in diameter.
1. mounting holes may be connected to ground.
1. mounting holes may be plated or non-plated through holes
1. must have ESD production on all inputs or optically isolate the module


