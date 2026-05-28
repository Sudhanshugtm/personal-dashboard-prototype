# Personal Dashboard — "For You" baseline

A static, mobile-first prototype of the imagined unified personal dashboard for
Wikipedia ([T419358](https://phabricator.wikimedia.org/T419358)): one "For You"
feed spanning reader, contributor, and moderator cards.

This is the **baseline** — a faithful reproduction of the current concept, kept
as the control that design variants are measured against.

## Live

Published via GitHub Pages — open on a phone for the real mobile experience.

## Built with

- [Wikimedia Codex](https://doc.wikimedia.org/codex/latest/) design tokens and
  CSS-only components (`cdx-button`, `cdx-icon`), loaded from CDN.
- No build step — plain `index.html` + `styles.css`.

## Notes

- Mobile-first: fills the screen like an app on a phone; shows inside a device
  frame on wider screens.
- Dark mode follows the OS via Codex's dark token sheet.
- Icons are placeholder SVGs (not yet the official Codex icon set).
