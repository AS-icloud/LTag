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

16) Short URL self-check: if what's typed into a "Short URL only" or vCard's info-URL field
   resolves to this app's own page (designer/index.html) rather than a separate info page or
   generated file, a red warning appears right under that field explaining why a finder would
   land back on the empty designer instead of your data, and pointing at "Generate info page
   (HTML)" (point 7) as the fix. This only checks for that one specific self-reference mistake
   — it can't verify a URL is reachable or correct in general.

17) Save / My Designs / history: "💾 Save" (top right) stores the entire current design —
   front + back shapes, every window, all Personal Details, QR settings, print setup — under
   a name you choose. "📂 My Designs" lists everything you've saved (newest first, with a
   count badge), each with Load / Rename / Delete. Loading replaces the whole workspace with
   that saved version. This is stored in this browser's local storage only — it does not sync
   between devices/browsers, and clearing site data/cookies removes it, so it's for quick
   in-progress checkpoints and reprint history, not permanent backup (export a PDF/PNG/print
   for that). There's no server, so nothing is uploaded anywhere.

18) Print border preview + Print Preview modal: every "Print this window's/shape's border"
   checkbox now visibly toggles a dashed on-screen outline as you click it (previously it only
   affected the final printed page, so there was no way to see the effect while designing).
   "👁 Preview" (top right, next to Save) opens a full on-screen mockup of exactly what Print /
   PDF / JPG / PNG will produce — true page size, margins, fold line, and border settings, all
   to scale — so you can check the final layout without committing to an actual print or file
   download.

19) Per-QR zoom preview: every QR-flagged window's card now has a "🔍 Preview this QR (full
   size)" button, right under its live capacity readout. It opens a large, clean rendering of
   that exact QR pattern at a fixed on-screen size (not shrunk to the window's real mm size on
   the tag), plus the exact data it encodes and which error-correction level is in use — a way
   to visually double-check contrast/pattern/quiet-zone before committing to print, especially
   for small or tightly-packed QR windows that are hard to eyeball at their true printed size.

20) New default starting design: the app now opens with a ready-made example instead of a
   near-blank canvas — a chamfered-corner 86 x 46mm tag (the shape you configured), Back
   enabled by default and folding from the top edge, with a caption text window plus a QR
   window on the front, and the same two windows mirrored onto the back (reflected across
   the shared fold edge, so a window close to the fold stays close to the fold on the other
   side too, and one far from it stays far on both). Front QR content defaults to "Short URL
   only" — deliberately left blank, since a placeholder URL would just be wrong once you
   actually host something; paste your real one in once you have it (see point 7). Back QR
   content now defaults to "Multilingual page" with the same 5 languages ticked as before —
   this one needs no manual setup, it builds its own working URL automatically from whatever
   Personal Details are filled in. "Back QR window(s) copy the front's QR content" is now
   OFF by default so the two sides can genuinely hold different content, as configured here.
   Edit or clear any of this the same way as before — it's a starting point, not a lock-in.

21) Print position on page: step 7 has a new "Position on page" choice — Top-left corner,
   Bottom-right corner, or Centered (the old default behaviour). Top-left places the design
   exactly Top-margin/Left-margin mm from those two page edges; Bottom-right does the same
   using the Bottom/Right margins instead; Centered ignores which corner and centers the
   whole design in the printable area like before. Default is Top-left with Top=10mm,
   Left=5mm (and Bottom=10mm/Right=5mm sitting ready if you switch to Bottom-right — flip
   the pill and it uses those without you having to re-enter numbers). Only applies to
   Virtual paper; Real/actual size always sizes the page tightly to the design, so there's
   no extra room to position within.

22) Mirror front windows to back: a second button next to "Copy front's outline to back" —
   "🪞 Mirror front windows to back" replaces ALL of the back's windows with a mirror image
   of the front's, reflected across whichever edge is picked as the fold direction (works for
   all four: top/bottom/left/right, not just top). A window close to the fold on the front
   ends up close to the fold on the back too (its own near edge), one far from the fold stays
   far on both sides, and rotation flips accordingly. It copies each window's size, image,
   text and font — but each copy keeps its own separate QR flag/content on the back, same as
   manually-added windows always have. This is a one-time snapshot (asks for confirmation
   first since it overwrites whatever's currently on the back), not a live link — move things
   afterwards on either side and the other side won't follow.

23) Front QR now defaults to your actual hosted info page: https://as-icloud.github.io/LTag/
   info-ankitsrivastava.html — the exact file you get from "Generate info page (HTML)" (see
   point 7), assuming it's uploaded to the root of that repo next to index.html. If your repo
   name or the filename changes, update the Short URL field to match.

24) Fixed: outline mirroring was a blind copy, now a true reflection. A tag with a back is
   one continuous piece folded over a single crease, not two separately-cut pieces — so the
   back's outline in the flat, pre-fold layout has to be the mirror image of the front's
   across that crease, not an identical clone. This only ever looked wrong for an asymmetric
   cut (a chamfered corner, a notch) — a plain rectangle or circle is already symmetric, so a
   clone and a true reflection look the same there. "⇄ Mirror front's outline to back" (step
   5) now does a real reflection using the same math as "Mirror front windows to back."
   Default shape updated to demonstrate this: an 86 x 46mm tag with a top-left chamfer on the
   front (top edge cut in from the left, left edge cut down to the middle, joined by a
   diagonal) and the matching bottom-left chamfer on the back — verified as an exact mirror,
   and that reflecting it a second time returns the original front shape. Default fold
   direction is now Bottom (back sits below front) to match.

25) PDF output scale correction (step 7): for apps that silently re-scale a PDF on their way
   to a printer with no way to turn it off (some label-printer apps, e.g. Phomemo, do this) —
   the PDF's page size and content were verified byte-for-byte correct (checked the actual
   generated PDF's page size and pixel content bounds directly: 148x210mm page, 86x46mm tag,
   exactly as designed), but an app can still shrink it after the fact on its way to the
   physical printer. This field inflates the PDF's own declared page size (and stretches the
   embedded image to match) by a percentage, so that after the external app's fixed shrink is
   applied, the physical result lands back on the true designed size. Defaults to 109.2% as a
   first-pass estimate from one reported measurement (86mm printed as 79mm) — re-measure your
   next physical print with a ruler and adjust this number if it's not exact: new % = (intended
   width ÷ measured width) × 100.

   Now also applies to JPG/PNG downloads (inflates their pixel dimensions by the same
   percentage — the only lever available for a plain bitmap, since it has no "declared
   physical size" field the way a PDF page does; only useful if whatever app opens it also
   does its own fit-to-target scaling based on pixel size). Print (the physical Print button)
   is NOT affected — it always matches the true design size exactly, since it goes straight to
   your OS print dialog rather than through an intermediate app that might re-scale it.

   Works the same regardless of paper size — A6/A5/A4, Virtual or Real/actual — since it's a
   percentage of whatever page size is currently selected, not a fixed number.

   Print Preview (👁 Preview) always shows the TRUE design size — Print will match it exactly.
   When this correction isn't 100%, the preview's note below the design says how much bigger
   the PDF/JPG/PNG downloads will come out compared to what's shown, so there's no surprise
   mismatch between what you see in Preview and what those three downloads actually are.

   UPDATE — this didn't fix it: after setting this to 109.2%, the physical Phomemo print still
   came out 80x42mm, barely different from the original uncorrected 79x42mm. That result only
   makes sense if Phomemo scales the WHOLE page down to some fixed physical output target,
   regardless of what mm size the PDF page declares itself to be — inflating the page and the
   design on it together, by the same percentage, doesn't change the design's fraction of the
   page (it was still 86mm design on a 161.6mm page = same ~53% either way), so Phomemo's own
   page (86mm design on a 148mm page = 58.1% either way, before or after the 109.2% inflation —
   both numerator and denominator scaled together), so Phomemo's own fixed-target scaling
   reproduces the same physical result every time. Defaulted back to 100% (see point 28 below
   for the actual fix attempt: switching paper mode instead of scaling it).

26) Square windows (including every QR window, since a QR pattern is always square) now show
   a single "Side length (mm)" field instead of separate Width/Height — set it once and both
   stay locked together. Dragging a square window's corner on the canvas also keeps it locked
   to a true square instead of letting it stretch into a rectangle. Rect windows are unaffected
   and still have independent Width/Height fields.

27) Default window layout re-synced to match your actual live-edited design (from your own
   screenshots): front has 3 windows — a name/address caption ("Srivastava.  Glasgow, UK" at
   X17/Y9, 56x10mm), a 25x25mm QR at X20/Y20, and a "Please scan this Qr code or the one on the
   back" note spanning the bottom (X0/Y0, 85x9mm). Back has just 1 window — a single large
   45x45mm QR at X21.17/Y1, no separate text window on the back. Personal Details and QR content
   settings were deliberately left untouched (only windows/positions/text were synced).
   IMPORTANT: there's no autosave — if you drag/resize windows directly in the live app and then
   refresh without pressing "💾 Save" first, it reverts to these defaults and your edits are
   lost. Click Save before refreshing, or before closing the tab, any time you've made changes
   you want to keep.

28) Default paper mode switched from Virtual A5 to Real/actual size, to actually fix the
   Phomemo print-shrink problem (see the "UPDATE" note under point 25 above for why the old
   scale-correction approach didn't work). Real/actual size builds a page sized to exactly your
   design plus the margins below (currently 96 x 113mm for this design) instead of a full A5
   sheet — the design fills ~90% of the page width instead of ~58%, which should leave a fixed-
   target-scaling app like Phomemo much less room to shrink it away. scaleCorrectionPct is reset
   to 100% as a clean baseline — print the next PDF, measure it, and if there's still a small
   residual shrink, recalibrate this number the same way as before (new % = intended width ÷
   measured width × 100), now specifically for this paper mode.

29) Phomemo auto-margin (step 7, Real/actual mode only): after 4 rounds of real physical test
   prints, the pattern was clear — Phomemo scales the WHOLE page to fit some fixed physical
   print AREA no matter what mm size the PDF declares (smaller declared page = bigger physical
   result, bigger page = smaller result). The "🖨 Auto-size page for Phomemo" checkbox (on by
   default) computes the Top/Bottom/Left/Right margins live from that calibrated target area, so
   the page always lands close to true size — for whatever tag dimensions are on screen, not
   just the specific 86x46mm design this was calibrated against. The margin fields grey out
   while this is on (they're being computed, not typed); untick it to set margins by hand again
   (e.g. printing through a normal, non-rescaling printer instead of Phomemo).

   The 4 real data points behind the calibration: declared page 148x210mm (A5) -> printed
   79x42mm; 96x113mm -> 133x70mm; 142x181mm -> 92x48mm; 150x191mm -> 88x46mm (closest, target is
   86x46). "Calibration target area (mm²)" is editable if a future print is still off — new area
   ≈ old area × (measured width ÷ intended width)². This is an empirical fit from one specific
   printer/app combo, not a manufacturer spec — a different label size loaded in Phomemo, or an
   app update, could shift it and need a fresh data point.

30) Front caption font size dropped 4.5mm -> 2.5mm (still bold) — the "Srivastava.  Glasgow, UK"
   text was overflowing its window and clipping the leading S and trailing K. The window also
   moved down 2mm (y 9 -> 7) so the smaller text sits properly within it. The front QR moved up
   1mm (y 18 -> 19) per your last two adjustment requests.

31) Polygon edge visibility (step 1 / step 5's Back Tag Shape section, only shown for Polygon
   shapes): a new checklist under the vertices box lets you show/hide individual outline
   segments — e.g. turning off just the diagonal chamfer line — without changing the shape's
   actual geometry or bounding box at all, on-screen and on every export/print. Default: the
   diagonal edge (edge 4) is now hidden on both front and back, per your request; all 4 straight
   edges still show. Rect/circle shapes are unaffected (no per-edge concept for them).

32) Fixed: copying info off the viewer page or the multilingual page (the "Copy" buttons) no
   longer lets phone numbers and emails get auto-detected and turned tap-to-call/tap-to-email by
   whatever app you paste into (Apple Notes being the classic case) — including right next to
   unrelated text like Notes, which is what made the whole pasted block look "clickable". Fixed
   by inserting an invisible zero-width character into phone/email values specifically in the
   copied text (not on the page itself — the page's own tel:/mailto: buttons are untouched and
   still tap-to-call/email as intended). Same approach used successfully in the earlier address
   label project. Applies to viewer.html, multilingual.html, and info-ankitsrivastava.html (the
   standalone generated info page, rebuilt fresh with this fix using the same personal data it
   already had baked in).

33) New "Custom paper" print mode (step 7, 3rd option next to Virtual paper and Real/actual
   size): type your actual physical paper's own Width/Height in mm — whatever sheet or roll
   is really loaded in your printer — then place the design anywhere on it, either by typing
   an exact Offset X/Y (mm from the paper's top-left corner) or by opening Print Preview and
   dragging the dashed blue box straight on the page. The two stay in sync live. No margins
   and no auto-sizing apply in this mode — the page is exactly the size you set, and the
   design sits exactly where you put it. The drag handle is a preview-only aid; it never
   appears in the actual Print/PDF/JPG/PNG output. The handle and the fit readout both turn
   red and warn if the design is dragged/typed off the edge of the paper. This is separate
   from and doesn't change the existing Phomemo auto-margin logic, which still only applies
   in Real/actual size mode.

34) Front QR default switched from "Short URL only" (needed a manually-uploaded HTML page and
   internet access to view) to "vCard contact" — fully offline, no hosting, no internet.
   Scanning it opens the phone's native "Add to Contacts" screen directly. Kept deliberately
   compact (name, mobile, email, and an English-only "if found, please contact" note) so it
   stays reliably scannable at a small 25mm QR window — a vCard with everything (both phones,
   both emails, both addresses, plus the 4-language safety note) comes to ~1000 bytes, which
   needs a QR pattern too dense to print reliably that small. The back QR is unaffected — it's
   now independent from the front's Personal Details (Back Tag section's "same as front" toggle
   is off by default) and keeps every field plus the full EN/ES/FR/DE message, since its QR
   window has much more physical room. Which fields count toward each QR is controlled by each
   field's own "in QR" checkbox in Personal Details (step 3) / Back Personal Details (step 5) —
   already-existing per-field toggles, just set differently for front vs back now. The vCard's
   safety-note language (Full / English only / None) is its own new picker in the QR Content
   section for whichever side is set to vCard — this is what actually saves the most space,
   since the 3 non-English lines are ~400 bytes on their own, more than every contact field
   combined.

SCOPE NOTES / WHAT WASN'T BUILT (flagging so nothing's a surprise)
- Outer polygon vertices are typed, not drag-editable on canvas (window shapes ARE drag +
  rotate editable; the tag's own outer polygon outline isn't, in this pass).
- The outer tag shape (front/back "Square" shape type, not windows) still shows independent
  Width/Height fields — set both the same. Windows are fixed as of point 26 above.
- Export is Print (browser print dialog, mm-accurate) plus Save as PDF / JPG / PNG, all on
  virtual A6/A5/A4 paper or real/actual custom-sized paper. PDF is a high-res raster image
  embedded on a correctly-sized PDF page (not vector line art) — sharp enough for QR
  scanning at normal print sizes, but not infinitely zoomable the way true vector PDF/SVG
  export would be. Standalone SVG file export wasn't built.
- All QR windows on one side (front or back) share that side's single QR content config —
  there isn't a separate content per individual window on the same side.
- The print layout places one copy of the design centered on the page (no auto-tiling to
  repeat multiple copies across a larger sheet).

Everything above was checked with coordinate-math unit tests and real (cairosvg) renders
of both the on-screen geometry and the print-page layout before delivery, not just eyeballed.
