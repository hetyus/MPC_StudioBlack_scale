# Binary Patch for AKAI MPC Software v2.15.1 (MPC Studio Black support)

Starting with version 2.10, AKAI changed the order of scales used in **Pad Perform mode**. However, this change was not reflected in the data sent to the MPC Studio Black controller. As a result, the controller’s LCD screen shows **incorrect scale names** compared to the actual scales selected in the software.

This patch corrects the issue by overwriting the relevant scale name table inside `MPC.exe` using a hex editor.

## Usage
1. **Make a backup** of your original `MPC.exe` (e.g. rename it to `MPC.exe.bak`).
2. Open `MPC.exe` in a **hex editor** (HxD on Windows, Hex Fiend on macOS).
3. Search for the scale names (e.g. `Major`, `Minor`, `Dorian`, `Chromatic`) in **UTF-16LE encoding**.
4. Locate the block containing all scale names in order.
5. Overwrite the strings according to the corrected order.
   - Keep each entry the same length as the original (pad with spaces if necessary).
6. Save the file and restart MPC Software.
7. The MPC Studio Black LCD should now display the correct scale names.

## Scale name order (before / after)
**Original (as stored in `MPC.exe`, wrong for Studio Black LCD):**

Major
Natural Minor
Harmonic Minor
Pentatonic Major
Pentatonic Minor
Blues
Flamenco
Gypsy
Hungarian Gypsy
Persian
Major Bebop
Whole Tone
Chromatic
Dorian
Phrygian
Lydian
Mixolydian
Aeolian
Locrian

**Corrected (patched order, matching actual software behaviour):**

Chromatic
Major
Natural Minor
Harmonic Minor
Pentatonic Major
Pentatonic Minor
Dorian
Phrygian
Lydian
Mixolydian
Aeolian
Locrian
Blues
Flamenco
Gypsy
Hungarian Gypsy
Persian
Major Bebop
Whole Tone

-> Corrected, with shorted text to match stirng length:

Chrom
Major
Natural Minor
Harmonic Minor
Pentatonic Major
PenMi
Dorian
Phryg
Lydian
Mixolyd
Aeolian
Locrian
Blues
Flamen
Gypsy
HGypsy
Persian
MjBebop
WhoTone

> **Important:** Each string must keep its original length in bytes.  
> If a replacement name is shorter, pad with spaces (UTF-16LE: `20 00`).  
> Do not shift the null terminator (`00 00`) or change record boundaries.
> String betweeen address 01e4d310 and 01e4d3d0

⚠️ **Disclaimer**  
This patch is unofficial and not supported by AKAI. Use at your own risk. Always make a backup of your original `MPC.exe` before applying any changes. The author(s) take no responsibility for data loss, malfunction, or other issues.

## Acknowledgements / References
- Discussions on various forums where MPC Studio Black users reported mismatched scale names after version 2.10.  
- Reverse engineering and patching inspired by community efforts around MIDI controllers and custom integrations.  
- Special thanks to the open-source community for tools like **HxD** (Windows) and **Hex Fiend** (macOS), which make binary inspection and editing practical.  
- Background info on the MPC Studio Black LCD SysEx protocol was shared by independent developers experimenting with custom controller scripts.
