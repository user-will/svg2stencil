# SVG2Stencil

3D print a solder paste stencil for any circuit board. Export the paste layer from KiCad as SVG and get a custom STL file you can 3D print.

![Example](example.png)

## Usage

1. Open `index.html` in a browser
2. Export your paste layer from KiCad: **File > Plot > F.Paste** (SVG format)
3. Drag and drop the SVG file onto the drop zone
4. Adjust stencil dimensions:
   - **Width/Height**: Overall stencil size (auto-sized to fit with 20mm margin)
   - **Thickness**: Stencil thickness (default 0.12mm)
5. Preview the stencil in the 3D viewer (drag to rotate, scroll to zoom)
6. Click **Download STL** to save

## Requirements

- Modern browser with WebGL support
- No installation or build step required

## Notes

- The tool parses filled SVG paths as apertures
- Apertures smaller than 0.1mm are filtered out
- STL files may need minor repair for 3D printing (most slicers handle this automatically)
