# Installation Instructions

## Installing via Pixi Global

To install with desktop shortcuts enabled:

```bash
pixi global install .
```

Or from the conda channel:

```bash
pixi global install -c conda-forge -c nandi-testing antigravity
# Then manually create the shortcut (see below)
```

## Installing via Conda

```bash
conda install -c nandi-testing antigravity
```

The conda package includes `menuinst` which will automatically create desktop shortcuts during installation.

## Fixing Missing Shortcuts after Pixi Global Install

If you installed via `pixi global` and don't see desktop shortcuts, it's because pixi global doesn't run conda post-link scripts. You have two options:

### Option 1: Manual Shortcut Creation

Create `~/.local/share/applications/antigravity.desktop`:

```ini
[Desktop Entry]
Name=Antigravity
Comment=Experience liftoff
GenericName=Text Editor
Exec=~/.pixi/bin/antigravity %F
Icon=antigravity
Type=Application
StartupNotify=false
StartupWMClass=Antigravity
Categories=TextEditor;Development;IDE;
MimeType=application/x-antigravity-workspace;
Actions=new-empty-window;
Keywords=vscode;

[Desktop Action new-empty-window]
Name=New Empty Window
Exec=~/.pixi/bin/antigravity --new-window %F
Icon=antigravity
```

### Option 2: Run menuinst manually

Find your pixi global environment prefix and run:

```bash
# Find the environment prefix
PIXI_ENV=$(find ~/.pixi -type d -name "*antigravity*" 2>/dev/null | grep envs | head -1)

# Run menuinst to create shortcuts
$PIXI_ENV/bin/menuinst-install
```

## Notes

- The `.conda` package includes `post-link.sh` and `pre-unlink.sh` scripts that use `menuinst` to manage desktop shortcuts
- These scripts work automatically with `conda install` but not with `pixi global install`
- For the best experience with shortcuts, use `pixi global install .` from this repository
