# Kodi PS5 binary add-ons

Generated PS5 packages, not upstream add-on source checkouts. Current runtime generation: `piers-ps5-1`.

Compatible Kodi PS5 builds include the stable repository. The testing repository ZIP linked by index.html is an explicit opt-in to unaccepted candidates. Build success and host export validation are not console acceptance. Packages are not generic FreeBSD binaries.

## Maintaining this repository

Use `tools/ps5/addon-repository.py` in the configured PS5 Kodi source checkout; see `docs/PS5-BINARY-ADDONS.md` there for prerequisites, the nested whitelist, source locks and stable-promotion evidence.

1. Run `python3 tools/ps5/addon-repository.py build --jobs 4`.
2. Rebuild/package the Kodi title when its candidate exports or runtime change.
3. Run `python3 tools/ps5/addon-repository.py package`.
4. Run `python3 tools/ps5/addon-repository.py publish --checkout PATH --commit`; add `--push` only when publication is intended.

Subsequent build/package runs can use `build --jobs 4 --package`. Upstream changes require an explicit `build --refresh-sources`. Never overwrite an existing package version: increment its PS5 revision. Stable promotion requires console evidence and approval of the exact ZIP SHA256. Retain matching sources, dependency sources and PS5 patches, and satisfy each package's license obligations before distribution.

The generated feeds are under `repo/<runtime>/stable` and `repo/<runtime>/testing`. Do not run the original template generator over them. Older package versions are retained. GitHub Pages is optional; repository definitions use raw GitHub URLs.
