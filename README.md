# Swift Toolchain for Android

This repository contains binary releases for the Swift Toolchain for Android.

The Swift Toolchain for Android is a complete toolchain for building Swift code for the Android platform. It supports all Android architectures, including 32-bit ones, and includes a complete port of the following components to Android:
- Swift compiler
- Swift Standard Library
- Dispatch library
- Foundation library (SwiftFoundation)

The toolchain also includes the SCADE Build Tool, which allows you to build and archive Swift SPM projects for Android with a single command. Read more about the SCADE Build Tool here:\
https://github.com/scade-platform/scade-build-tool

The Swift Toolchain for Android supports the following Swift versions: 5.8, 5.9, 5.10. The Swift 6.0 is in progress now and will be available soon.

## Installation

### Installation via Brew

The easiest way to install the Swift Toolchain for Android is by installing `scd`, the SCADE Build Tool, via the Homebrew package manager. The `scd` tool will install all the necessary components for building Swift code for Android. To install `scd` via Brew, run the following command:
```
brew install scade-platform/toolchain/scd
```

### Standalone package

The Swift Toolchain for Android can also be installed as a standalone package. This package includes the Swift compiler for Android as well as the `scd` build tool for building SPM projects.

You can download standalone package here:\
https://github.com/scade-platform/swift-android-toolchain/releases


## Usage

### Building an SPM project for Android platform
To build an SPM project for the Android platform, run the `scd build` command from the root of the SPM project and specify one of the Android platforms to build for:

```
scd build --platform android-arm64-v8a
```

This command will automatically install the Swift toolchain for Android and build the SPM project for the desired Android platform.


### Archiving an SPM project for Android

The `scd` build tool can build an SPM project for multiple Android platforms and archive it into a single directory suitable for embedding into Android projects. To create an archive, run the `scd archive` command with the set of Android platforms you want to build:
```
scd archive --platform android-arm64-v8a \
            --platform android-x86_64 \
            --platform android-armeabi-v7a \
            --platform android-x86
```

The resulting archive directory will be placed into the `lib` subdirectory of the current working directory. You can change the output directory using the -o argument.

### Archiving an SPM project into .aar library
The `scd` build tool can also archive an SPM project into an Android .aar library.

Archiving into an .aar library requires a valid `AndroidManifest.xml` located inside the SPM project root. The manifest should contain at least the package ID and version information:
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="com.example.scadeexample"
    android:versionCode="1"
    android:versionName="1.0">
</manifest>
```

To create an .aar archive, pass the additional `--type android-aar` argument to the `scd archive` command:
```
scd archive --type android-aar
            --platform android-arm64-v8a \
            --platform android-x86_64
```

## License

The Swift toolchain for Android contains an Android port of the original Swift compiler distributed under the Apache 2.0 license. The complete license text is in the Apache-2.0-LICENSE.txt file.
