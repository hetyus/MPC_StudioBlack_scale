# MPC_StudioBlack_scale
Binary Patch for AKAI MPC Software v2.15.1 (MPC Studio Black support)

Starting with version 2.10, AKAI changed the order of scales used in Pad Perform mode.
However, this change was not reflected in the data sent to the MPC Studio Black controller.
As a result, the controller’s LCD screen shows incorrect scale names compared to the actual scales selected in the software.

This patch corrects the issue by overwriting the relevant scale name table inside MPC.exe using a hex editor.

---

Usage

1. Make a backup of your original MPC.exe (e.g. rename it to MPC.exe.bak).
2. Open MPC.exe in a hex editor (HxD on Windows, Hex Fiend on macOS).
3. Search for the scale names (e.g. Major, Minor, Dorian, Chromatic) in UTF-16LE encoding.
4. Locate the block containing all scale names in order.
5. Overwrite the strings according to the corrected order.
6. Keep each entry the same length as the original (pad with spaces if necessary).
7. Save the file and restart MPC Software.
9. The MPC Studio Black LCD should now display the correct scale names.

---
DRAFT!!!:

Original (as stored in MPC.exe, wrong for Studio Black LCD):

Major
Harmonic Minor
Dorian
Phrygian
Lydian
Mixolydian
Aeolian
Locrian
Chromatic

String in ASCII: Major.
String in HEXA:

Corrected (patched order, matching actual software behaviour):

Chrom
Major
Minor
Dorian
Phrygian
Lydian
Mixolydian
Aeolian
Locrian

String in ASCII: Chrom.
String in Hexa:

