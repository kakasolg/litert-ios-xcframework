# litert-ios-xcframework

> **Superseded — archived.** Since LiteRT 2.3.2, upstream's `Package.swift` points its binary targets at prebuilt
> xcframeworks on the [LiteRT releases](https://github.com/google-ai-edge/LiteRT/releases) page, so you no longer
> need a self-built `CLiteRT.xcframework`. If SwiftPM fails to resolve upstream because of Git LFS
> ([LiteRT#8521](https://github.com/google-ai-edge/LiteRT/issues/8521)), the
> [kakasolg/LiteRT](https://github.com/kakasolg/LiteRT) fork carries the 2.3.2 package without LFS attributes:
> `.package(url: "https://github.com/kakasolg/LiteRT.git", exact: "2.3.2-spm-fix.1")`.
> The v1.0.0 release below (built from a 2026-08 LiteRT revision) stays available for existing users.

Prebuilt `CLiteRT.xcframework` — the C API of Google's
[`google-ai-edge/LiteRT`](https://github.com/google-ai-edge/LiteRT) for iOS/Metal,
built via `//litert/swift:CLiteRT` (`--config=ios_arm64 --compilation_mode=opt`).

This repo exists solely to host the built artifact as a public GitHub Release so it
can be consumed as a Swift Package Manager remote `binaryTarget` (`url:` + `checksum:`),
without requiring authentication — the source and full verification work live in
private research repos.

## Provenance / verification

- Source: `google-ai-edge/LiteRT`, reproducibility independently verified in a clean
  Xcode Cloud VM (fresh clone + Bazel build, symbols and structure matched byte-for-byte
  in functional output; see `kakasolg/litert-xcframework-verify`).
- Physical-device validated on iPhone Air (iOS 26.6): pair-similarity margin +0.1626,
  Recall@1/@3 = 0.398/0.620, MRR 0.926 (matches Android LiteRT-LM to 3 decimal places).
- Not affiliated with or endorsed by Google — this is an independently built artifact
  for personal SPM distribution convenience only.

## Usage

```swift
.binaryTarget(
    name: "CLiteRT",
    url: "https://github.com/kakasolg/litert-ios-xcframework/releases/download/<tag>/CLiteRT.xcframework.zip",
    checksum: "<sha256 from the release notes>"
)
```

## License

The built binary is derived from `google-ai-edge/LiteRT`, licensed under Apache 2.0.
See the [upstream repository](https://github.com/google-ai-edge/LiteRT) for full license terms.
