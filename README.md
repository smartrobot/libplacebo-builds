# libplacebo Build Scripts

This repository contains build scripts for compiling libplacebo as a dynamic library using Meson and wrap files.

## Features

- Cross-platform builds (Linux and Windows)
- Automated CI/CD with GitHub Actions
- Dynamic library output
- Meson wrap dependency management
- Automated testing

## Building Locally

### Prerequisites

**Linux:**
```bash
sudo apt-get update
sudo apt-get install -y python3-pip ninja-build pkg-config libvulkan-dev vulkan-validationlayers-dev spirv-tools
pip3 install meson
```

**Windows:**
```powershell
choco install python3 ninja pkgconfiglite vulkan-sdk
pip install meson
```

### Build Steps

1. Setup the build directory:
```bash
meson setup builddir --default-library=shared
```

2. Compile:
```bash
meson compile -C builddir
```

3. Test:
```bash
meson test -C builddir -v
```

4. Install:
```bash
meson install -C builddir --destdir=install
```

## Output Files

After building, you'll find:

**Linux:**
- Shared library: `builddir/subprojects/libplacebo/src/libplacebo.so`
- Headers: `builddir/subprojects/libplacebo/src/include/libplacebo/`
- Installed: `install/usr/local/lib/libplacebo.so`

**Windows:**
- Dynamic library: `builddir/subprojects/libplacebo/src/libplacebo.dll`
- Import library: `builddir/subprojects/libplacebo/src/libplacebo.lib`
- Headers: `builddir/subprojects/libplacebo/src/include/libplacebo/`

## CI/CD

The GitHub Actions workflow automatically:
- Builds on both Linux and Windows
- Runs tests
- Creates release artifacts
- Uploads to GitHub releases

## Dependencies

All dependencies are managed through Meson wrap files in the `subprojects/` directory. The main dependency is libplacebo itself, which is automatically downloaded and built.