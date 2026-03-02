# Fastfetchtosh

> A retro Apple–inspired Fastfetch layout for Zsh that blends Starship, Konsole, and a warm Gruvbox palette into a cohesive terminal experience.

## Highlights

- Custom Fastfetch layout with a bespoke ASCII logo and Gruvbox Rainbow Starship prompt.
- JetBrainsMono Nerd Font at 12 pt ensures precise glyph coverage for both Starship and Fastfetch.
- Konsole profile tuned for subtle transparency, truecolor accuracy, and a warm #2c2c2c background.
- Designed and tested on Arch Linux, but portable to any distro with Konsole, Fastfetch, and Starship installed.

## Requirements

| Component | Purpose |
| --- | --- |
| Zsh | Interactive shell where Fastfetch and Starship live. |
| Starship | Prompt engine that consumes the Gruvbox Rainbow preset. |
| Fastfetch | System info drawer responsible for the Apple-inspired layout. |
| Konsole | Terminal emulator providing the transparency and color control. |
| JetBrainsMono Nerd Font (12 pt) | Guarantees properly rendered Powerline/nerd glyphs. |
| Truecolor terminal | Needed for the precise color palette (#2c2c2c, #6d3100, etc.). |

## Installation steps

1. **Install the prerequisites**
   ```bash
   sudo pacman -S zsh fastfetch starship konsole ttf-jetbrains-mono
   ```
2. **Copy Fastfetch assets**
   ```bash
   cp config.jsonc apple-ascii.txt ~/.config/fastfetch/
   ```
   > The layout expects both files to live side-by-side under `~/.config/fastfetch/`.
3. **Apply the Starship Gruvbox Rainbow preset**
   ```bash
   curl -L https://starship.rs/presets/gruvbox-rainbow -o ~/.config/starship.toml
   ```
   Then source Starship inside your `~/.zshrc`:
   ```bash
   eval "$(starship init zsh)"
   ```
4. **Ensure JetBrainsMono Nerd Font is active** in Konsole (see Konsole section below).
5. **Optional:** Append `fastfetch` to `~/.zshrc` to show the layout on every shell startup.

## Konsole configuration

### Font

- Profile → **Edit Current Profile** → **Appearance** → **Font** → `JetBrainsMono Nerd Font`, **Size**: `12pt`.
- Nerd Font variant is mandatory for glyphs in Fastfetch and Starship.

### Colors & Transparency

| Setting | Value |
| --- | --- |
| Background | `#2c2c2c` |
| Intense Background | `#2c2c2c` |
| Faint Color | `#6d3100` |
| Background transparency | `3%` |
| Wallpaper transparency | `40%` |

> Konsole already supports truecolor, but double-check `Edit Current Profile → Appearance → Color → Enable transparency` for the subtle frosted look.

### Why these choices?

- The warm palette keeps the display legible while nodding to retro Apple color bursts.
- Low transparency (3%) maintains contrast on multicolored wallpapers.
- `#6d3100` provides that Gruvbox ember accent for highlights.

## Starship prompt

- The configuration uses the official Gruvbox Rainbow preset from Starship:
  https://starship.rs/presets/gruvbox-rainbow
- Place the preset in `~/.config/starship.toml` so the prompt automatically mirrors the terminal colors.
- Starship runs inside Zsh via `eval "$(starship init zsh)"` in `~/.zshrc`.

## Fastfetch layout

- Copy the `config.jsonc` and `apple-ascii.txt` files into `~/.config/fastfetch/`.
- The layout expects the ASCII logo file to sit alongside the JSON config.

```
~/.config/fastfetch/
├── config.jsonc
└── apple-ascii.txt
```

- Inside `config.jsonc`, every color reference uses hex values to control the presentation precisely.
- Fastfetch leverages the ASCII art to mimic a retro Apple startup screen while overlaying system stats.

## Optional startup behavior

To have Fastfetch run automatically whenever a new shell opens, add this to your `~/.zshrc`:

```bash
fastfetch
```

## Notes & Troubleshooting

- **Font mismatch** → Fastfetch and Starship rely on Nerd Font glyphs; missing glyphs usually mean the wrong font variant.
- **Color profile differences** → Konsole themes are per-profile; edit the active scheme to match the hex codes above.
- **Transparency issues** → Konsole’s blur/real transparency only works with compositing enabled (i.e., KDE/Plasma or another compositor).
- **Truecolor requirement** → Fastfetch and Starship outputs assume `COLORTERM=truecolor`. Verify with `printf '\x1b[38;2;255;100;0mTRUECOLOR\x1b[0m\n'`.

## Visual differences

Any discrepancy between setups is usually caused by:

1. Fonts that lack patched glyphs (switch to the Nerd Font release).  
2. Konsole’s color scheme diverging from the documented hex pairs.  
3. Transparency or compositor settings that forcibly darken the background.

## Summary

Fastfetchtosh delivers a warm, Apple-flavored terminal theme that pairs Starship’s rainbow prompt with a custom Fastfetch layout, all anchored in Konsole’s subtle transparency. Follow the configuration steps above, and you’ll have a cohesive, polished shell that feels both retro and modern—just the way the project intended.
