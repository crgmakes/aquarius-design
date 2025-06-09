# PCB Design Guidelines

So you would like to edit or create a PCB for Aquarius?? That's great! Please follow the guidelines below.

## General
---
1. Everything is designed in metric.
    
---

## Schematic
---

- Generally, all inputs on the right, all outputs on the left, power on the top, ground on the bottom.
- You may use KiCad symbols, but if you wish to customize them, please pull them into a CRG Make library first.
    * **DO NOT** customize them in the PCB!

---

## PCB
---

### Design Rules

+ Min Trace Width: 0.127 mm (5mil)
+ Min Power Width: 0.5mm (19.7mil)
+ Min Trace Spacing: 0.1524 (6mil)
+ Standard Via: 0.3/0.6mm (11.8mil/23.6mil)
+ Min Hole Size: 0.2mm (7.8mil)
+ Edge Cuts: 0.05mm
+ Min Text Height: 1mm

### General
+ All footprints should from the CRG Makes libraries.  **AVOID** using KiCad footprints directly.
    * Each footprint is optimized for our specific needs and DFM. If you need to change a footprint or need a new footprint, please contact us.
+ Each board must have a silkscreen text field for version. The label must be `<<tag>>`
+ Each board must have a silkscreen text field for the git hash. The label must be `<<hash>>`
+ Version and hash must be on the back. Version and hash may also be on the front.
+ All test points should be the back
+ All test points should be labeled by function.
+ All connectors must be labeled by function.
+ All connector pins should be labeled individually by function
+ Designator text should be horizonal; use vertical right when necessary.
+ KiBuzzard used for all negative text
+ Each board should have appropriate branding and labeling
+ Each board must have size dimensions specified on the User.Drawing layer
+ Each board nust have all edge connector locations defined on the User.Drawing layer
+ Each board must have all mounting hole locations defined on the User.Draing layer

---
