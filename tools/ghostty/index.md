# ghostty

Terminal emulator. Used as a plain container for herdr: no native tabs, splits or prefix keys to fight with.

- [config](config) - copy of `~/Library/Application Support/com.mitchellh.ghostty/config`

## Setup

1. Install: `brew install --cask ghostty`.
2. Create the config dir and copy [config](config) into it:
   ```bash
   mkdir -p ~/Library/Application\ Support/com.mitchellh.ghostty
   ```
3. Reload with `cmd+shift+,` inside Ghostty.

## Theme

Current: `Cutie Pro` (single fixed theme). List all bundled themes with `ghostty +list-themes`. The binary is not on PATH by default; call `/Applications/Ghostty.app/Contents/MacOS/ghostty +list-themes`. For a light/dark pair use `theme = dark:<name>,light:<name>`.

Docs: https://ghostty.org/docs
