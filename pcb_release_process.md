# PCB Release Process

This is the release process that must be followed to cut a new version of a PCB

## Process
---

1. Complete schematic and all routing
1. Perform ERC within schematic and clear all errors. Certain power/gnd errors are OK.
1. Perform DRC within PCB and clear all errors. There should be NO errors when complete.
1. Fix any issues now.
1. In schematic view, click Tools -> Edit Symbol Fields.
1. Carefully validate every part. Ensure manufacture part number (MPN) matches value and footprint precisely. Be maticulous.
1. Check all footprints to ensure they match the footprint expressed by the part number.
1. Do the previous two steps again. I know you telegraphed the response - don't. This will bite you in the ass later if you do.
1. Update PCB from Schematic (F8). Check for any issues.
1. Perform DRC within PCB and clear all errors. There should be NO errors when complete.
1. Perform PCB clean up - Tools -> Clean Up Tracks and Vias
1. Perform DRC within PCB and clear all errors. There should be NO errors when complete.
1. Check schematic and PCB into git.
1. Create pre-release build -- tag should indicate version and release candidate as 1. Example, v1.1-RC1. See release instructions.
1. Download artfacts for release and unzip.
1. Check panel images top and bottom for any issues. Focus on silkscreen and incorrect labels
1. Check panel drawing for any issues. Focus on fabrication labels, dimensions, or other silkscreen.
1. Check non-panel images top and bottom for any issues. Panel should have same issues.
1. Check non-panel drawing for any issues. Focus on fabrication labels, dimensions, or other silkscreen.
1. Check non-panel schematic for any issues. Very unlikley.
1. Check non-panel 3d model for any issues. Look for part rotation problems, offset issues, any missing 3d models.
1. Check non-panel renders top, bottom, and orthographic. Images and model issues should be reflected here. Note anything that is different!
1. Fix any issues found so far.
1. Check in and return to step 2. Yes, step 2.
1. Upload your gerber, bom, and cpl to https://jlcdfm.com
1. Check SMT layout -- focus on part orientation.
1. Check DFM for PCB -- focus on any trace to trace issues, drill size issues, and annular ring problems
1. Return to step 1 and fix any issues.
1. RESTART AT STEP 2. NO REALLY - do them all AGAIN. Trust me. You will thank me.
1. When everything checks, produce the final release using Git. See release instructions.
1. Download and produce PCB/PCBA as required.

## Notes
* Version numbers are defined by tags in Git
* Version numbers shall start with lower case v, primary version number, period, secondary version number - e.g., v2.1
* Part orientation problems in 3d model are likely issues WITHIN KiCad. Ensure every model is based in ${KICAD_USER_MODEL_DIR}.
* Part orientation problems during DFM are likely BOM/CPL problems. These can ONLY be fixed editing crgm.kibot.yaml, rotations section.
* Missing parts in 3d model could be a footprint problem in PCB, or wrong path (${KICAD_USER_MODEL_DIR}), or an actual missing model.




