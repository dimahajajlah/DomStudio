# DomStudio
DomStudio — Full Project Description
What it is
DomStudio is a browser‑based collage and wallpaper studio. You upload your own photos, freeform‑crop them into stickers (no rectangle limits), arrange everything on a giant white canvas alongside drawings, sticky notes, text labels, and a built‑in decorative sticker pack, and then download the finished composition as a high‑resolution 2880 × 1800 PNG sized exactly for a MacBook Retina wallpaper. It's frontend‑only — nothing leaves your browser.


The interface, top to bottom
1. Header bar
Logo + title "DomStudio" with the tagline "Crop freely. Compose freely. Export as wallpaper."
Upload Images button — opens the file picker; accepts multiple images at once (JPG, PNG, etc.).
Download Wallpaper button — exports the canvas as a 2880×1800 PNG. Greyed out until you've added at least one item.
2. Left sidebar (three sections)
a) Uploaded

Shows every image you've imported as a thumbnail grid (2 columns).
Hover any thumbnail to reveal two actions: Crop and Remove.
Empty state shows a dashed dropzone you can click to open the file picker.
b) Sticker Pack (built‑in decorations — 18 stickers)

Yellow star, pink star, purple sparkle, crescent moon, sun, red heart, pink heart, lightning bolt, cloud, rainbow, flower, smiley face, green checkmark, fire, diamond, crown, music note, leaf.
Each is a transparent SVG with bold colors and outlines so they read like real plastic/paper stickers.
Drag any sticker onto the canvas, or click to drop it in the center.
c) Cropped Stickers

Every cutout you create from your uploads lives here on a checkered (transparent) background.
Hover to reveal Add (drops it on the canvas) or Remove.
You can also drag them onto the canvas, or double‑click to add.
3. Canvas toolbar (above the canvas)
A row of five mode buttons. Picking one swaps the cursor and reveals contextual options on the right:

Select (default) — interact with items: drag, resize, rotate, delete.
Pen — freehand opaque drawing.Color swatches: black, purple, red, orange, green, blue, pink, white.
Size slider: 1 – 40 px.
Highlighter — freehand semi‑transparent drawing (35% opacity, so it layers like a real marker over things underneath).Color swatches: yellow, green, red, blue, pink.
Size slider: 8 – 80 px.
Sticky note — click anywhere on the canvas to drop a colored note.Color swatches: yellow, pink, blue, green, orange, lavender.
Text — click anywhere to drop a text label.Color picker (same palette as Pen).
Size slider: 16 – 200 px.
Above the canvas itself there's also a small status row showing the canvas dimensions (2880 × 1800 (MacBook wallpaper)) and a Zoom slider running from 15% to 100% (default 40%) so the huge canvas fits comfortably on your screen.


The freeform cropper
When you click Crop on an uploaded image, a fullscreen modal opens with the image centered. You get two cropping modes (not just rectangles):

Lasso — hold and drag to draw a freehand outline around any part of the image. Release to close the shape automatically.
Polygon — click to drop anchor points one at a time, building a multi‑sided shape; click the first point (or the Finish button) to close it.
Other cropper details:

A live preview of the path you're drawing.
Undo last point for polygon mode.
Reset to start the selection over.
Cancel to back out without saving.
Save Sticker clips the image to your shape and produces a transparent‑background PNG that lands in the Cropped Stickers panel — ready to drop on the canvas.

The canvas (the main workspace)
A fixed 2880 × 1800 white canvas, scaled to fit using the Zoom slider.
A subtle drop shadow makes it look like a physical board on the workspace.
All elements live in a single z‑ordered list, so a sticker, drawing, sticky note, and text label can all be reordered against each other. Selecting any item brings it to the front.
Pressing Delete or Backspace removes the currently selected item (ignored while you're typing into a sticky note or text box, so you don't lose text).
Item types on the canvas
Image stickers (cropped photos and pack stickers)

Drag to move anywhere.
Resize handle (bottom‑right) — keeps the aspect ratio.
Rotate handle (top‑center) — free 360° rotation around the sticker's center.
Delete handle (top‑left red ✕).
A purple selection outline appears when picked.
Sticky notes

Colored card with a soft drop shadow, defaulting to a 300×300 square.
Drag to move; resize handle (bottom‑right) for free width/height; rotate handle on top.
Double‑click to type — the whole note becomes an editable text area with auto‑wrapping.
Click outside (or blur) to commit the text.
Delete handle (top‑left red ✕).
Text labels

Plain text rendered directly on the canvas in your chosen color/size.
Drag to move; rotate handle on top; delete handle on the corner.
Double‑click to edit; multi‑line input is supported.
Selection shows a dashed purple outline so it doesn't visually compete with the text itself.
Pen / highlighter strokes

Drawn live as you move the pointer (mouse, trackpad, or touch).
Stored as smooth point paths and rendered as SVG with rounded line caps/joins for clean curves.
Highlighter strokes are drawn at 35% opacity so they tint everything beneath them.
Strokes participate in z‑order along with everything else.
How the modes feel
In Select mode, items are interactive (cursor becomes grab/move).
In Pen or Highlighter modes, items are passive — your pointer always paints. The cursor becomes a crosshair.
In Sticky note or Text modes, the cursor becomes a copy cursor; one click on empty canvas drops a new item at that exact spot, and the tool automatically returns to Select so you can immediately position or edit it.
Dragging a sticker out of the sidebar onto the canvas places it right where you drop it (centered on the cursor), regardless of zoom level.

Downloading the wallpaper
Hitting Download Wallpaper:

Creates an offscreen 2880×1800 canvas with a white background.
Walks every item in z‑order and renders it at full resolution:Stickers are drawn at their exact size and rotation around their center.
Sticky notes get a colored rectangle plus their drop shadow plus their text, word‑wrapped to fit the note's width.
Text labels are drawn line‑by‑line in their chosen color and size.
Strokes are stroked path by path with the right color, width, opacity, and round caps.
Exports the result as a PNG and triggers a browser download named wallpaper-<timestamp>.png.
The output is pixel‑perfect for a MacBook Retina display and works just as well as a regular desktop wallpaper, social post, or print.


Look & feel
Clean, modern UI with a purple primary color (HSL 262 83% 58%), neutral greys, and the Inter font throughout.
Generous use of icons (lucide) on every action so tools are recognizable at a glance.
Hover states, selection outlines, and drop shadows give the workspace a tactile, app‑like feel rather than a bare HTML page.

Under the hood (quick technical note)
Built as a React + Vite single‑page app.
Pure frontend — no server, no database, no accounts. Your images never leave the browser.
All canvas items share a single discriminated union (sticker | sticky | text | stroke) so the renderer, the selection logic, the keyboard shortcuts, and the PNG export all stay in sync as you add new content types.
Cropping uses HTML5 canvas clipping to produce true transparent PNGs from your freeform shapes.
Downloads are produced client‑side with canvas.toDataURL, so exports are instant and private.
That's the whole picture — every panel, tool, gesture, and what happens when you press the big purple Download Wallpaper button at the end.
