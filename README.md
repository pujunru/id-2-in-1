# ID 2-in-1

Combine two scans of an ID card (front and back) onto a single printable page.

**[Open the tool →](https://pujunru.github.io/id-2-in-1/)**

## Privacy

**Your images never leave your computer.** This is a single static HTML file with
no build step, no dependencies, no server, and no network requests of any kind —
no CDN, no analytics, no telemetry, no fonts. All image processing happens in your
browser via the Canvas API, and the PNG/PDF files are generated locally.

You can verify this yourself: read `index.html` (it's ~300 lines), or open your
browser's Network tab while using it and confirm nothing is sent.

Because it's fully self-contained, you can also just download `index.html` and open
it directly from disk, with your network turned off if you like. This is the
recommended approach for sensitive documents such as passports or ID cards.

## Usage

1. Scan both sides of the card and save them as images.
2. Drop, paste, or click to load them into the Front and Back panels.
3. Each side is auto-cropped from the scanner background. Use **Rotate 90°** for
   sideways scans, or adjust **Edge sens.** and hit **Re-crop** if the crop is off.
4. Set your page options and click **Build page**.
5. Download as PNG or PDF.

## Printing at true size

Output is 300 dpi. The default card width of 85.6 mm is the ISO/IEC 7810 ID-1
standard, so the printed result matches the physical card 1:1.

When printing, set scaling to **100%** / **Actual size** — do *not* use "Fit to
page", which will silently resize the card.

## Options

| Option | Notes |
| --- | --- |
| **Page** | A4 or US Letter. |
| **Layout** | Stacked vertically or side by side. |
| **Place** | Centered, or top-left against a fixed reference corner. |
| **Card width** | Physical width in mm. 85.6 mm is standard ID-1. |
| **Gap** | Space between the two cards. |
| **Margin** | Exact offset in top-left mode; a minimum in centered mode. |

Below ~5 mm of margin, many printers will clip the edge with their non-printable border.

## Auto-crop

The tool samples the four borders of the scan to learn the scanner background
color, then scans inward for the first row and column where enough pixels diverge
from it. This handles a card placed anywhere on the platen, against either a white
or a dark scanner lid.

It's an axis-aligned trim, so it corrects position but not rotation — a skewed scan
yields a bounding box with some background in the corners. Straighten the card on
the glass for best results. If detection fails, the full image is kept rather than
returning a bad crop.

## Browser support

Any current browser. No installation required.

## License

MIT — see [LICENSE](LICENSE).
