# Wezterm Theme Switcher

A script-based setup to **change Wezterm terminal themes** quickly via an interactive picker. Browse hundreds of built-in color schemes, preview them live, and apply your choice with a single keybinding.

## Features


https://github.com/user-attachments/assets/122bdce5-fa65-448e-9439-f3470809f8ef


- **Interactive theme picker** — Fuzzy search through themes with [fzf](https://github.com/junegunn/fzf)
- **Live preview** — See the selected theme applied to the terminal as you navigate the list
- **One keybinding** — `Ctrl+Shift+T` opens the switcher from inside WezTerm


## Requirements

- [Wezterm](https://wezterm.com/#Installation) installed
- **Lua** (usually provided by Wezterm or your system)
- **fzf** — install with your package manager, e.g. `sudo dnf install fzf` (Fedora) or `sudo apt install fzf` (Debian/Ubuntu)
- **bash**
- For the external launcher script: **wtype** (e.g. `sudo dnf install wtype` on Fedora)

### Installing fzf and Lua

| System        | fzf | Lua |
|---------------|-----|-----|
| **Debian / Ubuntu** | `sudo apt update && sudo apt install fzf` | `sudo apt install lua5.4` (or `lua5.3`) |
| **RHEL / Fedora**   | `sudo dnf install fzf` | `sudo dnf install lua` (on RHEL 8/9 you may need `lua51` or enable EPEL) |
| **Arch Linux**      | `sudo pacman -S fzf` | `sudo pacman -S lua` |

## Installation

1. **Use this as your Wezterm config directory**  
   Copy this project into `~/.config/wezterm/` so that Wezterm loads `wezterm.lua` from there.

   ```bash
   # Example: clone or copy this repo into the config dir
   cp -r /path/to/wezterm/* ~/.config/wezterm/
   ```

2. **Ensure scripts are executable** (optional, for direct use of `wezthemes.sh`):

   ```bash
   chmod +x ~/.config/wezterm/scripts/wezthemes.sh
   ```

3. **Install fzf and Lua** if needed — see the table above for your distribution.

## How to Use

### From inside Wezterm

1. Press **`Ctrl+Shift+T`**.
2. A pane opens on the right with an fzf list of themes; the current theme is shown in the prompt.
3. Move with arrow keys or type to filter; the terminal **previews** the theme as you move the selection.
4. Press **Enter** to **apply** the highlighted theme and close the picker.
5. Press **Escape** to **cancel** and keep your current theme; the pane closes and the window restores to its original size.

Or add an alias (e.g. in `~/.bashrc` or `~/.zshrc`):

```bash
alias wezthemes='touch /tmp/wezterm_trigger_theme_switcher'
alias wt=wezthemes
```

Then run `wezthemes` or `wt`.

## Customization

- **Default theme** — Edit `globals.lua` and set `current_theme` to the name of any theme listed in `theme.lua` (e.g. `"Adventure"`, `"Catppuccin Mocha"`).
- **Theme list** — Add or remove entries in `theme.lua`; names must match Wezterm’s built-in color scheme names (see Wezterm docs or the existing list).
- **Keybinding** — In `wezterm.lua`, change the key in the `keys` table (e.g. the entry with `action = wezterm.action_callback(theme_switcher)`). You can also change the other keys to match your preferences. 

## Notes

- The scripts under `scripts/` assume the config directory is `~/.config/wezterm/`. If you use another path, set `wezterm.config_dir` accordingly or adjust the paths in those scripts.
- The theme list in `theme.lua` uses Wezterm’s built-in scheme names; no extra theme files are required.
