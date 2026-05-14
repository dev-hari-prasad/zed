---
title: Desktop Dev and Build Commands
description: "Quick commands to run and build Zed for desktop development."
---

# Desktop Dev and Build Commands

This repository now provides Cargo aliases for common desktop workflows.

## Run a development desktop build

From the repository root:

```sh
cargo zed-dev
```

This starts Zed using the `zed` crate in development mode.

## Build a release desktop binary

From the repository root:

```sh
cargo zed-build
```

This builds a release binary for the `zed` crate.

## Install on Linux desktop

If you want the app integrated with your Linux desktop (`~/.local/bin` and `.desktop` files):

```sh
./script/install-linux
```

## Notes

- You must install system dependencies first (see the platform-specific development docs).
- On Linux, `script/linux` installs required system packages.
