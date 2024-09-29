Supported Platforms
=========================

This page documents the status of various platforms and renderers supported by Godot.

## Table of Contents

**Operating Systems**
* [Windows](#windows)
* [Linux](#linux)
* [macOS](#macos)
* [Android](#android)
* [IOS](#ios)
* [Steam Deck](#steam-deck)
* [HTML / WebGL](#webgl)

**Renderers**
* [Forward+ / Vulkan](#vulkan)
* [Forward+ / Direct3D 12](#d3d12)
* [Forward+ / Metal](#metal)
* [Mobile / Vulkan](#mobile)
* [Compatibility / OpenGLES 3](#compatibility)

## Windows

Fully supported. See [renderers](#supported-renderers).

## Linux

Fully supported. See [renderers](#supported-renderers).

## macOS

Godot and Terrain3D work fine on macOS, however Apple security is overly aggressive when using the release binaries.

Users have reported errors like this:

`"libterrain.macos.debug" cannot be opened because the developer cannot be verified. macOS cannot verify that this app is free from malware.`

Running the following commands within the downloaded and unzipped directory appears to resolve the issue.

```
$ xattr -dr com.apple.quarantine addons/terrain_3d/bin/libterrain.macos.debug.framework/libterrain.macos.debug
$ xattr -dr com.apple.quarantine addons/terrain_3d/bin/libterrain.macos.release.framework/libterrain.macos.release
```

You can also [read comments and workarounds](https://github.com/TokisanGames/Terrain3D/issues/227)
from other users. 

If disabling Apple security is not working, or if approaching a release date, macOS users should [build from source](building_from_source.md) so you can sign the binaries with your own account.

## Android

As of Terrain3D 0.9.1 and Godot 4.2, Android is reported to work. 

* Use textures that Godot imports (converts) such as PNG or TGA, not DDS.
* Enable `Project Settings/Rendering/Textures/VRAM Compression/Import ETC2 ASTC`.

The release builds include binaries for arm32 and arm64.

There is a [texture artifact](https://github.com/TokisanGames/Terrain3D/issues/137) affecting some systems using the demo DDS textures. This may be alleviated by using PNGs as noted above, but isn't confirmed.

Further reading:
* [Issue 197](https://github.com/TokisanGames/Terrain3D/issues/197)

## IOS

As of Terrain3D 0.9.1 and Godot 4.2, iOS is reported to work with the following setup:

* Use textures that Godot imports (converts) such as PNG or TGA, not DDS.
* Enable `Project Settings/Rendering/Textures/VRAM Compression/Import ETC2 ASTC`.
* Set `Project Settings/Application/Config/Icon` to a valid file (eg `res://icon.png` or svg).
* The Terrain3D release includes iOS builds, however they aren't signed and may not work.
* If needed, build the iOS library and make sure the binaries are placed where identified in `terrain.gdextension`:
```
     scons platform=ios target=template_debug
     scons platform=ios target=template_release
```

* Select `Project/Export`, Add the iOS export preset and configure with `App Store Team ID` and `Bundle Identifier`, then export.

```{image} images/ios_export.png
:target: ../_images/ios_export.png
```

Once it has been exported, you can open it in XCode, run locally, or on your device.

Further reading:
* [Issue 218](https://github.com/TokisanGames/Terrain3D/issues/218)
* [PR 219](https://github.com/TokisanGames/Terrain3D/pull/219)
* [PR 295](https://github.com/TokisanGames/Terrain3D/pull/295)


## Steam Deck

As of Terrain3D v0.9.1 and Godot 4.2, the first generation Steam Deck is reported working, running the demo at 200+ fps.

The user got it working with the following:
* Use SteamOS 3.5.7
* Install `glibc` and `linux-api-headers` in addition to the standard Godot dependencies
* [Build from source](building_from_source.md)


Further reading:
* [Issue 220](https://github.com/TokisanGames/Terrain3D/issues/220#issuecomment-1837552459)


## WebGL

Terrain3D does export to WebGL, however it requires the [Compatibility Renderer (read more)](#compatibility).


Supported Renderers
====================

* [Forward+ / Vulkan](#vulkan)
* [Forward+ / Direct3D 12](#d3d12)
* [Forward+ / Metal](#metal)
* [Forwad Mobile](#mobile)
* [Compatibility / OpenGLES 3](#compatibility)

## Vulkan

The Forward+ Vulkan renderer is fully supported.

## D3D12

The Forward+ Direct3D 12 renderer was recently merged into Godot 4.3 and is not yet supported by Terrain3D. Early testing shows artifacts.

## Metal

Support for Apple's Metal for iOS and macOS was recently merged into Godot 4.4-dev1. It is not yet supported by Terrain3D. No testing has been done.

## Mobile

The Forward Vulkan Mobile renderer is fully supported in Terrain3D 0.9.3. There is a precision artifact in 0.9.2.

## Compatibility

The OpenGLES 3.0 Compatibility renderer has recently reached "feature complete" status in Godot 4.3. Features are still lacking in 4.2.

It is not yet fully supported by Terrain3D. The terrain mesh builds and is reported to work fine. The remaining issue is that the texturing shader and the mouse cursor do not work due to the lack of necessary features.

Some work has been done to partially support Compatibility in Godot 4.2 and full support coming in Terrain3D 0.9.4 with Godot 4.3+.

Further reading:

* [Issue 217](https://github.com/TokisanGames/Terrain3D/issues/217)