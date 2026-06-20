# ingeniousfrog/homebrew-tap

Personal [Homebrew tap](https://docs.brew.sh/Taps) for apps and CLI tools published under the [ingeniousfrog](https://github.com/ingeniousfrog) GitHub account.

**Live repo:** https://github.com/ingeniousfrog/homebrew-tap

## Install (users)

```bash
brew tap ingeniousfrog/tap
```

### GUI apps (Casks)

```bash
brew install --cask cachebar
```

### CLI tools (Formulas)

```bash
brew install mollow
```

Upgrade later:

```bash
brew update
brew upgrade --cask cachebar
brew upgrade mollow
```

Uninstall:

```bash
brew uninstall --cask cachebar
brew uninstall mollow
brew untap ingeniousfrog/tap   # optional, if nothing else from this tap is installed
```

## What is in this tap?

```text
homebrew-tap/
  Casks/
    cachebar.rb      # CacheBar (GUI)
  Formula/
    mollow.rb        # Mollow (CLI)
  README.md
```

**Yes — you can reuse this same tap for other apps and CLI tools.** Add another cask or formula, push, and users install with:

```bash
brew install --cask <name>   # GUI .app bundles
brew install <name>          # CLI binaries
```

Naming rules:

- Cask file: `Casks/myapp.rb` → `brew install --cask myapp`
- Formula file: `Formula/myapp.rb` → `brew install myapp`
- Use lowercase and hyphens (Homebrew convention)

## Maintainer: update Mollow after a release

1. Publish [Mollow GitHub Release](https://github.com/ingeniousfrog/Mollow/releases) assets (tag `v<version>`).
2. From the **Mollow** repo:

   ```bash
   ./packaging/update-homebrew-sha256.sh <version>
   ./packaging/push-homebrew-tap.sh
   ```

   Or copy `packaging/homebrew/mollow.rb` to `Formula/mollow.rb` in this repository and push.

## Maintainer: update CacheBar after a release

1. Upload `CacheBar_<version>_aarch64.dmg` to [CacheBar GitHub Releases](https://github.com/ingeniousfrog/CacheBar/releases) (tag `v<version>`).
2. From the **CacheBar** repo, print the checksum:

   ```bash
   ./scripts/print-dmg-sha256.sh release/CacheBar_<version>_aarch64.dmg
   ```

3. Edit `Casks/cachebar.rb`: `version`, `sha256` (and `url` if the pattern changes).
4. Push to **homebrew-tap**:

   ```bash
   ./scripts/push-homebrew-tap.sh
   ```

   Or commit directly in the `homebrew-tap` repository.

## Maintainer: add a new app to this tap

1. Create `Casks/<app-token>.rb` for GUI apps or `Formula/<app-token>.rb` for CLI tools.
2. Point `url` at a stable GitHub Release (or other HTTPS) asset; set `sha256`.
3. For casks, set `app "<Name>.app"` to match the bundle inside the DMG.
4. Commit and push to `homebrew-tap`.
5. Document in that project’s README:

   ```bash
   brew tap ingeniousfrog/tap
   brew install --cask <app-token>   # GUI
   brew install <app-token>            # CLI
   ```

CLI tools use `Formula/`; GUI `.app` bundles use **Casks**.

## Notes

- This tap is **not** [homebrew-core](https://github.com/Homebrew/homebrew-cask); you maintain it yourself.
- `cachebar` cask is **Apple Silicon only** (`depends_on arch: :arm64`).
- `mollow` formula supports macOS (Apple Silicon and Intel) and Linux x86_64.
- Unsigned GUI builds may still need **Open Anyway** on first launch (same as manual DMG install).

## Sync from source repos

- CacheBar: the `homebrew-tap/` folder in [ingeniousfrog/CacheBar](https://github.com/ingeniousfrog/CacheBar) is a source template for casks.
- Mollow: use `packaging/homebrew/mollow.rb` and `./packaging/push-homebrew-tap.sh` from [ingeniousfrog/Mollow](https://github.com/ingeniousfrog/Mollow).
