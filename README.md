# Stroke-following spatial error

Touch positions from a T1 board C log, compared with the Prusa multi-layer crosshatch G-code.

The nearest-line search reports a maximum of about 0.47 mm on this file. The hatch pitch is 1 mm, so a touch that is farther than 0.5 mm from the stroke being drawn is closer to a neighboring stroke, and the search scores that neighbor. This project keeps the same point-to-segment distance and scores each touch against the G1 stroke the machine is drawing.

On the strokes the sensor actually covers:

| | Mean | RMS | Max | Share above 0.5 mm |
| --- | ---: | ---: | ---: | ---: |
| Nearest line (original scaling) | 0.094 mm | 0.125 mm | 0.465 mm | 0% |
| Horizontal, stroke follow | 0.352 mm | 0.504 mm | 3.191 mm | 22.1% |
| Vertical, stroke follow | 0.625 mm | 0.791 mm | 4.655 mm | 56.0% |

The sensor X axis is mirrored relative to the printer. Its footprint is about X 145.9–173.0 mm and Y 153.3–185.2 mm, inside a drawing that runs to 178.7 × 188.8 mm. Strokes off that footprint are left out of the statistics. Samples stuck on a coordinate rail (22.5, 292.5, or 337.5) are clipped and left out as well.

## Run the viewer

```bash
npm install
python3 analysis/spatial_error.py
npm run dev -- --hostname 0.0.0.0 --port 43123
