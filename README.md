# Alice39s/scoop-bucket

[![Tests](https://github.com/Alice39s/scoop-bucket/actions/workflows/ci.yml/badge.svg)](https://github.com/Alice39s/scoop-bucket/actions/workflows/ci.yml) [![Excavator](https://github.com/Alice39s/scoop-bucket/actions/workflows/excavator.yml/badge.svg)](https://github.com/Alice39s/scoop-bucket/actions/workflows/excavator.yml)

Scoop manifests for [xmtr](https://github.com/Alice39s/xmtr), a concurrent traceroute that maps every hop on [xmsl.dev IPMap](https://xmsl.dev/ipmap).

```powershell
scoop bucket add alice39s https://github.com/Alice39s/scoop-bucket
scoop install alice39s/xmtr
```

The manifest installs the release binary for x86_64, x86 and ARM64.

## Updates

- The xmtr release workflow writes the new manifest on every release.
- Excavator runs `checkver` every four hours and commits any version the release workflow did not write. It reads the hashes from the release's `SHA256SUMS`.

## Checks

On every push and pull request, CI does the following:

- It validates each manifest against the Scoop schema and file rules (`bin/test.ps1`).
- It installs xmtr with Scoop on Windows x64, x86 and ARM64 runners.
- It runs `xmtr --version` and traces `127.0.0.1`, then uninstalls xmtr.

The `bin/` scripts are the wrappers from Scoop's bucket template, so the Scoop tools can be run locally:

```powershell
.\bin\checkver.ps1 xmtr       # latest release and the manifest's version
.\bin\checkhashes.ps1 xmtr    # download each architecture and compare hashes
.\bin\formatjson.ps1          # apply Scoop's JSON layout
```
