# litert-ios-xcframework

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
