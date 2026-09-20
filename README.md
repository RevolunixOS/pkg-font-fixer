# font-fixer

Experimental workstation helper that scans `/nix/store` for OpenType and
TrueType fonts, copies them into `~/.local/share/fonts/store`, and resets the
ownership and permissions of that directory.

> [!CAUTION]
> The current script uses `sudo`, hard-codes the owner as `gabriel:users`, and
> recursively changes permissions. It is not portable or safe to run unchanged
> under another account. Edit `src/font-fixer` before use.

## Build

```bash
nix build github:RevolunixOS/pkg-font-fixer
```

The derivation installs both the `font-fixer` command and a desktop entry.

## Intended workflow

After adapting the username and group, run:

```bash
font-fixer
fc-cache -f
```

The script copies font files out of immutable Nix store paths so applications
that only inspect conventional per-user font directories can discover them.
This duplicates files and may collect fonts from unrelated store closures.

## Recommended improvements

- derive ownership from `id` rather than a fixed username;
- avoid `sudo` for files under the invoking user's home directory;
- select fonts from explicit package outputs instead of scanning the whole
  store;
- add a dry-run mode and tests.

## License

See [`LICENSE`](LICENSE).
