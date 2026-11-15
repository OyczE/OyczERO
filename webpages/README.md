# Public web output

This directory will contain the built static GitHub Pages site, browser
flasher, public help and release catalog. Keep site assets relative to the
deployment base path. Deploy this directory's public build, not the parent
development checkout or the whole distribution staging tree.

Development source remains in `apps/updater/`. Export only the reviewed
HTML/CSS/JavaScript/assets required by the browser. Omit source maps, debug
fixtures, credentials and environment files. Large downloads link to Release
assets; they are not copied into the Pages deployment.

No runnable website or flasher has been exported here yet.
