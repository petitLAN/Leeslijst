# Reading room

An original, account-free reconstruction of the spine-to-cover interaction shown in Bookshelf.so's public launch screenshots. The live original returned HTTP 401 and no original source repository was located. This project does not include Bookshelf.so's original code.

## Open and personalize

Open `index.html` in the ZIP, or `dist/index.html` in the source project, in any modern browser. Click a spine to pull the book forward without moving its neighbors. Swipe or drag the foreground book horizontally to view the back cover. Swipe again to view the front. Click the foreground book to put it back. Left/right arrow keys turn the book when it has keyboard focus. Escape also returns it. Use the previous/next buttons and arrow keys. Use **Edit collection** to rename the shelf, clear the example collection, add books, upload covers, write reviews and rate books. Search, category filters and favorites work locally.

Changes are stored in this browser's localStorage. They do not sync to other visitors or devices. **Download website** exports a standalone HTML file containing the current collection and uploaded covers. Publish this downloaded HTML as `index.html` on any static host to show that collection to everyone. JSON export/import provides portable backups. No application accounts, database, API keys, external scripts or network requests are required.

## Source

All markup, styles, interactions and sample data live in `dist/index.html`. The `bookshelf-data` JSON script contains the starting collection. Local saved data takes precedence over that seed. Remove the `reading-room-v1` localStorage key or import JSON when replacing an existing browser collection.

Books are CSS 3D objects with front, spine, back and page surfaces. The selected book moves into a separate foreground layer and rotates into a three-quarter view; shelf slots stay fixed. Reduced-motion preferences disable transitions. Cover uploads are resized to at most 600 pixels high / 500 pixels wide and embedded as JPEG data URLs. Default covers are typographic placeholders, not original published cover artwork.

The app itself has no authentication. The initial managed deployment has the default private hosting access; the downloaded static HTML can be hosted publicly with no authentication.

## Painted archive theme

The dark theme combines a hand-painted library backdrop, angular ink marks, copper details and illustrated book decals on the existing CSS 3D book meshes. Theme CSS is maintained in `art/theme.css` and embedded in the standalone HTML. The background artwork is generated with the built-in image tool and is embedded as a WebP data URL so downloaded HTML works offline. `art/painted-archive.webp` preserves the project asset. Uploaded covers, user notes, click targets and the click-again-to-close interaction are preserved.

The foreground book is rendered in a separate layer while its original 34px shelf slot remains reserved. The shelf stays at the same position and scale while the selected book moves into the foreground. Swipe gestures are handled with Pointer Events and do not trigger the return click. A separate back-cover description can be edited for every book and is preserved in HTML/JSON exports. Example descriptions are original short summaries, not reproduced publisher copy. Long descriptions appear in full in the panel below the back-facing book.

Book rotation now tracks horizontal pointer displacement directly during dragging. Release snaps to the nearest front/back face, with a short velocity projection for flicks. Each extraction resets its source pose with transitions disabled. Shelf and foreground spines share the same projection: foreground rotation around the 95px book center is compensated by -95px depth at 90 degrees before the shelf book is revealed. Source coordinates are measured from the static foreground layout origin, never its previously animated bounding rectangle.
