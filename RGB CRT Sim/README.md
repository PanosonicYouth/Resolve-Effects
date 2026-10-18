# RGB CRT Sim

A CRT monitor look for DaVinci Resolve, built as a Fusion macro that works on the Edit page. It rebuilds the red/green/blue phosphor pattern of a CRT, then adds the imperfections that make it read as a real tube: scanlines, chromatic aberration, vignetting, curved lens distortion, glow and reflections.

The phosphor structure is deliberately larger than a real CRT's so the effect survives on modern high-resolution footage and compression.

## Installation

1. Download `RGB CRT Sim.drfx` from the Releases page.
2. Double-click the file and follow the DaVinci Resolve install prompt.
3. Restart Resolve.
4. On the Edit page, find **RGB CRT Sim** in the Effects library and drag it onto a clip or an adjustment clip.

## How it works

The signal flows through the controls in this order:

1. **Effects (noise):** signal noise is added first, so it gets "displayed" by the CRT like a real signal would.
2. **Effects (aberration):** chromatic aberration is applied to the image.
3. **CRT Config:** the picture is turned into red, green and blue phosphor triads.
4. **Effects (scanlines, vignette, lens, rays, reflections):** these finish the look.
5. **Levels:** colour and brightness correction to compensate for what the previous steps took away.

The controls are in three tabs: **CRT Config**, **Effects** and **Levels**.

---

## CRT Config

This tab controls the phosphor mask, the grid of red, green and blue dots that makes up a CRT picture.

| Control | What it does |
|---|---|
| **Horizontal Triads** | The number of RGB triads across the image. Lower values give bigger, chunkier triads and a stronger effect. Default 240. |
| **Vertical Cells** | The number of phosphor cells down the image. Default 207. |
| **Phosphor Width** | How much of each triad's width the lit phosphor fills. Lower values leave larger dark gaps. Default 0.7. |
| **Phosphor Height** | The same as Phosphor Width, but vertically. Default 0.7. |
| **Edge Softness** | How soft or sharp the edges of each phosphor are. Default 0.08. |
| **Column Offset** | Staggers alternating columns vertically, giving the offset dot pattern seen on many tubes. Default 0.5. |
| **Brightness Compensation** | Makes up for the light lost by masking the image into phosphors. Raise it if the picture is too dark. Default 2.8. |
| **Blur** | A blur applied after the mask. Its job is to offset moiré. Raise it if you see moiré patterns, lower it for a sharper mask. Default 1. |

**Tip:** the triad and cell counts are set lower than a real CRT's on purpose, to exaggerate the effect. Keep them lower for stylised results or for viewing at small sizes. Raise them for a subtler look at full resolution. The pattern can produce moiré when it interacts with fine detail or with scaling. Increase **Blur** to counter it, and check the result at 100% zoom as well as in the fitted viewer.

---

## Effects

These controls help sell the CRT look.

### Noise

Noise is added *before* the CRT mask, so it goes through the phosphor pattern like real signal noise.

| Control | What it does |
|---|---|
| **Signal Noise** | The amount of noise. Default 0.33. |
| **Signal Noise Scale** | The size of the noise grain. Default 0.7. |

### Aberration

Colour fringing, strongest towards the edges of the frame.

| Control | What it does |
|---|---|
| **Center / Width / Height / Soft Edge** | Position and size of the region kept free of aberration, with a soft edge. Aberration is applied outside it, so these control how far into the frame the fringing reaches. |
| **Aberration Distance** | How far the colour channels are pushed apart. Default 0.02. |
| **Aberration Strength** | The overall strength of the fringing. Default 1. |

### Scanlines

| Control | What it does |
|---|---|
| **Scanline Frequency** | The number of scanlines. Default 6.66. |
| **Scanline Sharpness** | How crisp the lines are. Default 0.8. |
| **Blend** | How strongly the scanlines are multiplied onto the picture. Default 0.439. |

### Vignetting

| Control | What it does |
|---|---|
| **Vignetting** | How much the corners and edges darken, as on a real tube. Default 0.396. |
| **Vignetting Aspect** | Shapes the vignette horizontally or vertically. Default 1.8. |

### Lens Distortion / Sizing

| Control | What it does |
|---|---|
| **Distortion Amount** | The curvature of the screen. Negative values bulge the image outwards like a curved CRT glass. Default -0.4. |
| **Center** | The centre point for the transform. |
| **Size** | Scales the image to fill the frame after distortion pulls the edges in. Default 1. |

### Rays / Reflections

Glow and glass reflections on the screen.

| Control | What it does |
|---|---|
| **Decay / Weight / Exposure / Threshold** | Shape the light rays (bloom) that spill from bright areas. Threshold sets how bright something must be to glow. |
| **Brightness** | The strength of the screen reflections. Default 0.236. |
| **Anamorphism** | Stretches the reflections. Default 2.866. |
| **Colorize** | How strongly the reflections pick up colour. Default 0.598. |

---

## Levels

The mask, scanlines and aberration all take light and colour away. These controls bring the picture back to where you want it.

### Initial Temp Correction

| Control | What it does |
|---|---|
| **Temperature** | The white balance before the CRT mask. Default 7050. |
| **Gain / Gamma** | Initial brightness and midtone adjustments. Defaults 1.7 and 0.86. |

### First Pass Colour / Gain Compensation

A colour wheel applied after the mask. Use Hue, Saturation and the Tint Angle and Length controls to remove or add any colour cast the phosphor mask introduces.

### Final Pass Colour

A final colour wheel for the overall tint of the image. Use Tint Angle and Length for colour, and Saturation to taste.

---

## Tips

- Apply the effect to an **adjustment clip** so it covers a whole timeline.
- If the picture is too dark, raise **Brightness Compensation** first. If it is too green or magenta, use the colour wheels in Levels.
- If you see moiré or shimmering, raise **Blur**.
- For a cleaner, more modern monitor, lower the noise, aberration and distortion, and increase the triad and cell counts.

## Credits

Created by *(your name here)*. Made for DaVinci Resolve.