# Kodi PS5 binary add-ons

Generated PS5 packages, not upstream add-on source checkouts. Current runtime generation: `piers-ps5-1`.

Compatible Kodi PS5 builds include the enabled stable repository and the testing repository, disabled on first discovery. Enable Kodi PS5 Testing Add-ons under My add-ons > Add-on repository to opt in to unaccepted candidates; the testing repository ZIP linked by index.html also remains available for manual installation. **Upgrade Kodi to the native shared-runtime title before installing these packages.** Legacy titles are unsupported; do not install the runtime marker separately. Build/package qualification is not console acceptance. Packages are not generic FreeBSD binaries.

## Maintaining this repository

Use `tools/ps5/addon-repository.py` in the configured PS5 Kodi source checkout; see `docs/PS5-BINARY-ADDONS.md` there for prerequisites, the nested whitelist, source locks and stable-promotion evidence.

1. Run `python3 tools/ps5/addon-repository.py build --jobs 4`.
2. Verify the upgraded shared-runtime Kodi title against the prepared SDK.
3. Run `python3 tools/ps5/addon-repository.py package --title-app <stage>/app`.
4. Review `python3 tools/ps5/addon-repository.py publish --checkout PATH --dry-run`, then run `python3 tools/ps5/addon-repository.py publish --checkout PATH --apply-native-migration --commit`; add `--push` only when publication is intended.

Subsequent build/package runs can use `build --jobs 4 --package --title-app <stage>/app`. Upstream changes require an explicit `build --refresh-sources`. Never overwrite an existing package version: increment its PS5 revision. Stable promotion requires console evidence and approval of the exact ZIP SHA256. Retain matching sources, dependency sources and PS5 patches, and satisfy each package's license obligations before distribution.

The generated feeds are under `repo/<runtime>/stable` and `repo/<runtime>/testing`. Do not run the original template generator over them. The native-only migration removes legacy binary packages in the owned feed scope. GitHub Pages is optional; repository definitions use raw GitHub URLs.
