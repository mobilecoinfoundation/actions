# MobileCoin Foundation - Common GitHub Actions

This repository exists to provide a central repository for shared actions.

## Install the SGX SDK

The `sgxsdk` action installs Intel's SGX SDK under `/opt/intel/sgxsdk`, verifies
the installer against Intel's SHA256 manifest, and exports `SGX_SDK`, `PATH`,
`PKG_CONFIG_PATH`, and `LD_LIBRARY_PATH` for subsequent steps.

The optional `version` input selects the installer version and defaults to
`2.17.101.1`. Without a `release` input, the download directory is derived from
the first two components of `version`, preserving the existing URL behavior:

```yaml
- uses: mobilecoinfoundation/actions/sgxsdk@main
  with:
    version: 2.25.100.3
```

For patch releases, set `release` to Intel's release directory separately from
the installer version. For example, SDK `2.30.101.1` is published under `2.30.1/`:

```yaml
- uses: mobilecoinfoundation/actions/sgxsdk@main
  with:
    version: 2.30.101.1
    release: 2.30.1
```

The action selects the Ubuntu installer matching the runner's distribution
version. Downloads or checksum verification failures stop installation.
