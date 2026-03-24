# SVG2Stencil

3D print a solder paste stencil for any circuit board. Export the paste layer from KiCad as a Gerber or SVG file and get a custom STL file you can 3D print.

Optionally add a **board lip** — a wall around the edge of the PCB that lets the stencil seat itself automatically without manual alignment.

![Example](printastencil.png)

## Usage

1. Open `index.html` in a browser
2. Export your paste layer from KiCad:
   - **Gerber (recommended):** File > Fabrication Outputs > Gerbers, enable F.Paste
   - **SVG:** File > Plot > F.Paste, select SVG format
3. Drag and drop the file onto the paste layer drop zone (or click to browse)
4. Adjust stencil dimensions:
   - **Width/Height**: Overall stencil size (auto-sized to fit with 20mm margin)
   - **Thickness**: Stencil thickness (default 0.12mm)
   - **High detail (resin)**: Enable to include apertures smaller than 0.1mm — off by default since FDM printers can't reliably print them, but resin printers can
5. Preview the stencil in the 3D viewer (drag to rotate, scroll to zoom)
6. Click **Download STL** to save

### Adding a board lip (auto-alignment)

A board lip adds walls that hang below the stencil and wrap around the PCB edges, so the stencil seats itself on the board without needing to be manually aligned.

1. Export the edge cuts layer from KiCad:
   - **Gerber:** File > Fabrication Outputs > Gerbers, enable Edge.Cuts — produces `*Edge_Cuts.gbr` or similar (`.gm1`, `.gko`)
   - **SVG:** File > Plot > Edge.Cuts, select SVG format
2. Drag and drop the edge cuts file onto the **Edge Cuts Layer** drop zone
3. The **Board Lip** section will appear with three controls:
   - **Lip Height**: How far the wall extends below the stencil (default 1.2mm)
   - **Wall Thickness**: Thickness of the lip wall (default 1.2mm)
   - **Fit Clearance**: Gap between the lip's inner face and the PCB edge (default 0.15mm) — increase if the fit is too tight
4. When the lip is enabled the stencil is automatically sized to the board outline — it won't extend beyond the edge of the PCB

If your board has interior cutouts (keychain holes, slots, etc.) the outermost contour is automatically selected as the board outline.

## Supported File Formats

### Gerber (RS-274X)
Accepts `.gbr`, `.ger`, `.gtp`, `.gbp`, `.gm1`, `.gko`, and other common Gerber extensions. Supports:
- Standard aperture types: circle (C), rectangle (R), obround (O), polygon (P)
- KiCad's `RoundRect` aperture macro for rounded rectangle pads
- Pre-instantiated aperture macros (KiCad 6+)
- Region fills (G36/G37) for polygon-defined apertures
- Stroke-based edge cuts with linear and arc segments (G01/G02/G03)
- Both metric (mm) and imperial (inch) units

### SVG
Accepts `.svg` files exported from KiCad's plot function. Parses filled paths as paste apertures and stroke-only paths as edge cuts outlines.

## Requirements

- Modern browser with WebGL support
- No installation or build step required

## Notes

- Apertures smaller than 0.1mm are filtered out by default — enable **High detail (resin)** to include them
- When the board lip is enabled the STL contains the stencil and lip as a single merged solid
- STL files may need minor repair for 3D printing (most slicers handle this automatically)
