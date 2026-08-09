LUGGAGE TAG DESIGNER 2 — built from scratch per your spec

Open index.html (upload this whole folder's contents — not the folder itself — to GitHub
Pages/Netlify, or open the file directly for testing — installable "Add to Home Screen"
PWA needs HTTPS hosting). Named index.html so it loads automatically at your site's root
URL (e.g. https://username.github.io/repo-name/) with no extra path needed.

WHAT'S HERE
- index.html      The entire app (single file: shape designer, windows, QR, front/back).
- viewer.html     Unchanged from the earlier project — the online info page a "Personal
                   Details" QR points to. Reused as-is since it already does exactly this job.
- multilingual.html  The translated 2-column info page a "Multilingual" QR points to.
- manifest.json, sw.js, icon*  PWA install/offline support.

HOW IT MATCHES WHAT YOU ASKED FOR

1) Shape designer: front tag shape is Rectangle / Square / Circle / Polygon, sized in mm.
   Polygon vertices are entered as one "x,y" per line (mm) rather than dragged individually
   — full vertex-dragging on the outer outline wasn't built in this pass, noted below.

2) Coordinate system: bottom-left corner of whichever shape you're looking at is always
   (0,0); X right, Y up. The header's cursor readout updates live as you move over the
   canvas and tells you which panel (front/back) you're over plus its local mm coordinate.

3) Windows: add rectangle/square/circle windows, each positioned either by its bottom-left
   corner or its center, sized in mm (or radius for circles), rotated by dragging the small
   dot above each window or by typing a degree value. Drag the shape itself to move it;
   drag the small amber square at its corner to resize it (right edge for a circle, since
   it only has a radius) — this respects whatever rotation the window is currently at, so
   the handle always tracks the visual corner, not the un-rotated one. Click to select,
   then arrow keys nudge by 1mm (0.1mm with Shift), Delete removes it.

4) Image + text: each window can hold an image, text, or both, with text placed top / bottom
   / left / right of the image, or directly over it. Font family, size (mm), weight, style,
   color and alignment are all exposed per window.

5) QR sizing/capacity: flag any window as "Use as QR code" and it shows, live, the max QR
   version and character capacity at all four error-correction levels (L/M/Q/H) for that
   window's current size, using the standard ISO 18004 byte-mode capacity table — plus
   whether your currently configured QR content actually fits. A solid white quiet-zone
   margin (default 4 modules) is always drawn around the QR automatically; the minimum
   module size and quiet-zone width are both editable in step 6.

6) Personal Details: same field set as before (name, org, two addresses, two mobiles, two
   phones, two WhatsApp numbers, two emails, notes), each with its own "in QR" checkbox.

7) QR content + info-page URL: pick what any QR-flagged window encodes — short URL only,
   an online "Personal Details" page (points at viewer.html with the data attached, so a
   finder with internet sees a clean tap-to-call/copy page), a fully offline vCard (builds
   BEGIN:VCARD straight from Personal Details, opens the phone's native Add-to-Contacts
   screen, no internet needed), plain text, or WiFi.

   Whatever gets printed is exactly what stays encoded in that QR forever — printing
   doesn't touch a database or a server, so there's nothing to change after the fact.
   A multi-line address or note keeps its own line breaks intact everywhere: in the
   offline vCard (via vCard's own line-break escaping, so Contacts apps show it exactly
   as typed instead of squashed onto one comma-separated line), in the online info page
   and its Copy button, and in the Multilingual preview and its Copy buttons.

   "Short URL only" holds exactly what's typed into that field — nothing else — which
   keeps a small front QR reliable to scan. If you still want it to open a page showing
   your details (not just a bare link), click "Generate info page (HTML)" right under
   that field: it downloads a standalone copy of viewer.html with your ticked Personal
   Details baked directly into the file (no long ?d=... query string). Upload that one
   file next to viewer.html on GitHub, then paste its URL into the Short URL field. The
   front QR then stays short and fixed while still landing on a full data page — same
   idea as the original address-label project, adapted to a static GitHub Pages site
   (no backend to look data up by a short code, so the data has to live in that one
   small file instead).

8) Back tag: toggle "This design has a back", pick which edge it folds from (top / left /
   right / bottom), and it's placed and gapped correctly next to the front for print. Back
   gets fully independent shape + windows + drag/keyboard editing. "Copy front's outline to
   back" copies only the physical shape/size to match the front — it deliberately leaves
   windows, QR flags and data alone, since those are yours to decide for the back; add
   windows there the same way you did on the front (buttons + drag to move/resize/rotate),
   then set each one's own content. Its Personal Details and QR content can either mirror
   the front's or be entirely different (see "Back QR window(s) copy the front's QR
   content" further down that section).

9) Layout: left half is every control (scrollable), right half is the live preview, matching
   the split you asked for.

10) Virtual printer (step 7): choose A6 / A5 / A4, portrait or landscape, with independent
   top/bottom/left/right margins in mm — defaults are 2mm left/right, 10mm top/bottom. The
   whole design (front + back, correctly gapped) is centered inside the printable area and
   drawn at true 1:1 mm scale on its own dedicated print layout, separate from the on-screen
   editor view, so the interactive drag handles/selection outlines never show up on paper.
   A live readout under the margin fields tells you if the current design fits that page —
   if it doesn't, Print asks for confirmation before overflowing the edge. In your print
   dialog use "Actual size / 100%" (not "Fit to page"), same as before.

11) Windows are corner-resizable directly on the canvas: select a window and drag the
   small amber square at its corner (right edge for a circle window) to change its size,
   in addition to typing exact numbers in the Width/Height/Radius fields. This respects
   the window's current rotation, so the handle always sits at the actual visual corner.
   "Back QR window(s) copy the front's QR content" (in step 5) still lets the back reuse
   the front's QR data/URL if you want that, once you've added a QR window to the back
   yourself — mirroring the outline no longer does this automatically, see point 8 above.

12) Print-border toggles: every shape now has its own "print border" checkbox sitting
   right next to that shape's own dimensions — front tag outline, back tag outline, and
   each individual window (including QR windows), all independently. Off by default for
   windows (so a text/image box doesn't print an unwanted rectangle around it), on by
   default for the front/back tag outlines (so you get a cut/fold guide unless you turn
   it off). This only affects the printed page — the on-screen editor keeps its usual
   light outline for every window/shape regardless, purely so you can still see and grab
   things while designing.

13) Fold-allowance line: the gap between front and back (now labelled "Fold allowance"
   in step 5, same field as before, still fully editable in mm) always shows a dashed
   guide line at its exact midpoint on screen, oriented correctly whichever edge you
   folded from (horizontal for top/bottom, vertical for left/right). A separate "Print
   the fold-allowance line" checkbox in step 7 (Print Setup) controls whether that line
   actually appears on the printed page — on by default.

14) Virtual vs real/actual paper, and PDF/JPG/PNG export: step 7 now has a "Paper mode"
   toggle. "Virtual paper" is the A6/A5/A4 + orientation behaviour from before. "Real /
   actual size" builds a custom page sized exactly to your design plus the margins you set
   — no fixed paper choice, no wasted space, meant for label printers or die-cut sheets.
   Both modes work with all four header actions: Print (to a physical printer), and Save
   as PDF / JPG / PNG (all three rasterize the exact same print layout at ~300dpi-equivalent
   resolution and trigger a download — PDF pages are sized to match the chosen paper
   exactly, so "Actual size / 100%" isn't even a concern for the PDF).

   Saved file names follow this pattern:
     Virtual paper:      Name_Virtual_PaperSize_Orientation.format
                          e.g. AnkitSrivastava_Virtual_A5_Portrait.pdf
     Real/actual size:    Name_WIDTHxHEIGHTmm_Orientation.format
                          e.g. AnkitSrivastava_192x71mm_Landscape.png
   "Name" comes from the Name field in Personal Details (falls back to "Tag" if empty),
   with spaces and punctuation stripped. Orientation in real/actual mode is inferred from
   whichever of width/height ends up larger, since there's no page to choose an orientation
   for.

15) Multilingual QR content type (best for the back — it has more room): pick "Multilingual
   (translated info page)" as the QR content type and tick which languages should be offered
   — Spanish, French, German, Italian and Portuguese are ticked by default, but any of the
   11 available (add Hindi, Punjabi, Arabic, Chinese, Japanese) can be swapped in/out; at
   least 5 must stay ticked or the QR won't generate (a red note tells you why). Scanning
   this QR opens multilingual.html (new file, included in the zip), which shows the finder's
   chosen language's labels next to your Personal Details, with a dropdown to switch language,
   Copy buttons for the data, and the same tap-to-call/WhatsApp/email/map/Save-as-Contact
   actions as the online info page.

   Right there in the designer, under the QR content section, is a live "what a finder will
   see" preview: the actual QR (scan it and it goes to the real multilingual.html URL, no
   placeholder), the destination URL in full, and two side-by-side columns — Original (English)
   on the left, Translated on the right — built from exactly the Personal Details fields you've
   ticked "in QR", using the same field labels and layout as multilingual.html itself. A
   dropdown above the right column picks which of your ticked languages to preview; Copy
   buttons under each column copy that column's data as plain text, ready to paste into a
   phone's Notes app or anywhere else.

SCOPE NOTES / WHAT WASN'T BUILT (flagging so nothing's a surprise)
- Outer polygon vertices are typed, not drag-editable on canvas (window shapes ARE drag +
  rotate editable; the tag's own outer polygon outline isn't, in this pass).
- "Square" windows/tags don't auto-lock width=height as you type — set both the same.
- Export is Print (browser print dialog, mm-accurate) plus Save as PDF / JPG / PNG, all on
  virtual A6/A5/A4 paper or real/actual custom-sized paper. PDF is a high-res raster image
  embedded on a correctly-sized PDF page (not vector line art) — sharp enough for QR
  scanning at normal print sizes, but not infinitely zoomable the way true vector PDF/SVG
  export would be. Standalone SVG file export wasn't built.
- All QR windows on one side (front or back) share that side's single QR content config —
  there isn't a separate content per individual window on the same side.
- No local tag-history/save-library — that was a v1 feature, not part of what you specced.
- The print layout places one copy of the design centered on the page (no auto-tiling to
  repeat multiple copies across a larger sheet).

Everything above was checked with coordinate-math unit tests and real (cairosvg) renders
of both the on-screen geometry and the print-page layout before delivery, not just eyeballed.
