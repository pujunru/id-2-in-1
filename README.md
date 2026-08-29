# ID 2-in-1

Two browser-based image tools that never upload your files:

1. **ID 2-in-1** — combine two scans of an ID card (front and back) onto a single printable page.
2. **HEIC → JPEG** — batch-convert iPhone HEIC/HEIF photos to JPEG.

**[Open the tool →](https://pujunru.github.io/id-2-in-1/)**

## Privacy

**Your images never leave your computer.** There is no server, no upload, no
analytics, no telemetry, and no third-party CDN. All processing happens locally in
your browser via the Canvas API, and the output files are generated on your machine.

The only network requests the page can make are for its own two local files,
`vendor/libheif.js` and `vendor/libheif.wasm`, and only when you open the
HEIC tab. The ID 2-in-1 tool loads nothing at all.

You can verify this yourself by opening your browser's Network tab while using it.

For sensitive documents such as passports or ID cards, the safest option is to
download this repo and open `index.html` from disk — it works fully offline.

## Usage — ID 2-in-1

1. Scan both sides of the card and save them as images.
2. Drop, paste, or click to load them into the Front and Back panels.
3. Each side is auto-cropped from the scanner background. Use **Rotate 90°** for
   sideways scans, or adjust **Edge sens.** and hit **Re-crop** if the crop is off.
   For full control, tick **Manual crop**: the whole scan is shown with a
   selection box you can drag, resize from any corner, or redraw by dragging on
   an empty area. It starts from whatever auto-crop found and follows the image
   when you rotate. Press **Apply crop** to confirm — the preview then shows the
   cropped result. **Edit crop** reopens the box, and **Reset to full** restores
   the entire scan.

   For a scan that is skewed or shot at an angle, tick **Free transform** while
   editing: the four corners become independently draggable. Put one on each
   corner of the card and press **Apply crop** — the quadrilateral is warped back
   into a straight rectangle, correcting the skew rather than just boxing it in.
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

Auto-crop is an axis-aligned trim, so it corrects position but not rotation — a
skewed scan yields a bounding box with some background in the corners. For those,
use **Manual crop → Free transform**, which corrects skew properly. If detection
fails, the full image is kept rather than returning a bad crop.

## HEIC → JPEG

Drop, paste, or pick one or more `.heic` / `.heif` files. Each is decoded and
converted to JPEG, then saved individually or all at once.

| Option | Notes |
| --- | --- |
| **Quality** | JPEG quality, 50–100. Default 92. |
| **Max edge** | Downscale so the longest side is at most this many pixels. 0 keeps the original size. |

Because browsers other than Safari cannot decode HEIC natively, a build of
[libheif](https://github.com/strukturag/libheif) is bundled in `vendor/` and used
to decode in-browser. It is loaded lazily — only when you open this tab — so the
ID 2-in-1 tool stays instant. On Safari, the system decoder is used as a fallback.

Note that JPEG has no transparency and is lossy, and that converted files keep no
EXIF metadata — which also means location data in the original is not carried over.

## Browser support

Any current browser. No installation required.

## Third-party code

`vendor/libheif.js` and `vendor/libheif.wasm` are unmodified build artifacts from
[libheif-js](https://www.npmjs.com/package/libheif-js) v1.19.8, distributed under
the LGPL. See `vendor/LICENSE.libheif`. Everything else is MIT.

## License

MIT — see [LICENSE](LICENSE).
