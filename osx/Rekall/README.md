# Rekall macOS GUI Application

This directory contains the macOS GUI application for Rekall, a memory forensics framework.

## Prerequisites

- Xcode (version depends on deployment target - see Compatibility section)
- macOS development environment
- x86_64 architecture support

## Building

### Required Setup

Before building, you need to create the `dist/rekal` directory structure that the build script expects:

```bash
# From the root of the rekall repository
mkdir -p dist/rekal
```

### Build Commands

Build the Rekall.app for x86_64 architecture:

```bash
xcodebuild -project Rekall.xcodeproj \
           -configuration Release \
           CODE_SIGNING_REQUIRED=NO \
           CODE_SIGN_IDENTITY="" \
           ARCHS=x86_64 \
           MACOSX_DEPLOYMENT_TARGET=10.11 \
           build
```

For modern macOS compatibility, you can also use:

```bash
xcodebuild -project Rekall.xcodeproj \
           -configuration Release \
           CODE_SIGNING_REQUIRED=NO \
           CODE_SIGN_IDENTITY="" \
           ARCHS=x86_64 \
           MACOSX_DEPLOYMENT_TARGET=10.13 \
           build
```

### Output

The built application will be located at:
```
build/Release/Rekall.app
```

## Notes

- The project is configured for x86_64 architecture only
- Code signing is disabled for development builds
- The `dist/rekal` directory is required but ignored by git (must be created manually)
- The application requires the MacPmem kernel extension for full functionality

## Compatibility

- **Original Design**: macOS 10.9+ with deployment target flexibility up to 10.11
- **Xcode Requirements**: 
  - For `MACOSX_DEPLOYMENT_TARGET=10.11`: Compatible with most Xcode versions
  - When using modern Xcode versions (like 26.0+) they no longer include libarclite for older deployment targets (10.9 to 10.11)
- **Architecture**: x86_64 only (ARM64 requires additional inline assembly fixes)

## Related Components

- MacPmem kernel extension: `../../tools/osx/MacPmem/`
- Core Rekall framework: `../../rekall-core/`