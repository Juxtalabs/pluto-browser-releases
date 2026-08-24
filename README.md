# Pluto Browser — releases

Public distribution point for **Pluto Browser** installers and the update manifests
the browser reads to know when a newer version exists.

This repository holds **no source code**. It contains only:

- `standard/‹platform›.json` — small manifests the browser polls (version + download URL + sha256)
- GitHub **Releases** — the actual installer files, attached as release assets

## Channel

| Channel    | Manifest                  | Build                        |
|------------|---------------------------|------------------------------|
| `standard` | `standard/win-x64.json`   | The shipping locked product  |

`standard` is the product. The old `no-login` channel is retired. Each installed
browser is built for exactly one channel and reads only that channel's manifest;
the channel is compiled into the binary and never changes for that install.

## Manifest shape

```json
{
  "version": "0.9.5",
  "url": "https://github.com/Juxtalabs/pluto-browser-releases/releases/download/v0.9.5/PlutoBrowserSetup.exe",
  "sha256": "‹64-hex lowercase over the installer›",
  "notes": "- What changed.\n- More."
}
```

The `url` points at an asset on this repo's own GitHub Release. The browser only
trusts downloads under `https://github.com/Juxtalabs/`.

## How an update ships

1. Bump the version in the source repo and build the installer on the build machine.
2. Create a GitHub Release here (`vX.Y.Z`) and attach the installer.
3. Update `standard/win-x64.json` to point at the new version + sha256.

The publish script in the source repo (`scripts/deployment/publish-release.sh`)
does all three. Every running browser notices within a few hours, or immediately
via **Settings → About → Check for updates**.
