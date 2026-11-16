# GitHub Pages content

This directory will contain the built static GitHub Pages site, browser
flasher, public help and release catalog. Keep site assets relative to the
deployment base path. Deploy this directory's public build, not the parent
development checkout or the whole distribution staging tree.

In this distribution repository, configure **Settings > Pages > Deploy from a
branch**, select **main** and **/docs**, then save. The local path is
`github/docs/`; it is separate from the private source repository's `docs/`.

Development source remains in `apps/updater/`. Export only the reviewed
HTML/CSS/JavaScript/assets required by the browser. Omit source maps, debug
fixtures, credentials and environment files. Large downloads link to Release
assets; they are not copied into the Pages deployment.

This README is the current placeholder entry page. No browser flasher or
installer interface has been exported here yet.

Current staged build: `20261116T173028Z-g2c142df3759d`.
See the [release notes](../releases/20261116T173028Z-g2c142df3759d/RELEASE-NOTES.md)
and [installation guide](../releases/INSTALL.md). The package is staged locally;
these links describe it but do not provide a published image download.
