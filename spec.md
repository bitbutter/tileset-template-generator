reference: https://www.boristhebrave.com/permanent/24/06/cr31/stagecast/wang/blob.html

# Blob Tileset Template Generator

A single-file web app that generates a downloadable PNG template image for 2D game blob/wang tilesets (thick walls). Artists open it in a browser, configure their tileset, and download a template to paint over.

## Overview

- **Format**: Single standalone `.html` file (inline JS + CSS, no dependencies, no build step)
- **Output**: Downloadable PNG image — a complete blob tileset template with variation slots
- **Tileset type**: Full 47-tile blob tileset (8-bit wang tiles for thick/fat walls)

## Inputs (Form UI)

### Required
- **Tile width** (px): width of a single tile
- **Tile height** (px): height of a single tile

### Variation Counts
- **Global default**: a single number input setting the default variation count for all tiles (minimum 1 = just the base tile)
- **Category overrides**: numeric inputs that override the global default for specific tile categories:
  - **Center** (tile 255 — fully connected fill tile)
  - **Straight edges** (tiles with one flat side: N, S, E, W)
  - **Inner corners** (concave corner tiles)
  - **Outer corners** (convex corner tiles)

## Tile Rendering

Each tile slot in the template is rendered as follows:

- **Size**: matches the user-specified tile width × height
- **3×3 bitmask indicator**: each tile displays a small 3×3 grid showing its connection bitmask
  - **Connected directions**: shown in **red**
  - **Unconnected directions**: shown in **white**
  - The center cell of the 3×3 grid always represents the tile itself
- **No index labels or numbers** on the tiles
- **Checkerboard grid overlay**: a faint checkerboard pattern across the entire image to show tile boundaries

## Layout

- Tiles are **packed tight** — no spacing/padding between tiles
- The layout follows the compact arrangements from the reference site (6×8 or 7×7 packing discovered by Caeles at OpenGameArt.org)
- **Variation slots** are placed **adjacent** to their base tile (extending the row)
- Each variation slot shows the **same bitmask** as its base tile (so the artist knows what shape to paint)
- **Colored 1px border** around groups of tiles that are variations of each other, to visually distinguish variant groups

## Output

- **PNG only**, no transparency needed
- Single "Download" button on the page
- The downloaded image contains the full tileset template ready for the artist to paint over

## Non-goals

- No figure/ground color rendering (no yellow/blue tile previews — only bitmask indicators)
- No SVG export
- No tile index numbers on tiles