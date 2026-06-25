# Compass Cyclic Primitives

![Development Status](https://img.shields.io/badge/status-active--development-blue.svg)

The lossless projection between `Compass.Cardinal` and the cyclic group `Cyclic.Group.Static<4>` (ℤ/4ℤ) — clockwise rotation expressed as addition in the group.

---

## Quick Start

The four cardinal directions form a cyclic group: rotating 90° clockwise is the same operation as adding `1` in ℤ/4ℤ, and four rotations return to the start. This package makes that isomorphism explicit, projecting any `Compass.Cardinal` onto a `Cyclic.Group.Static<4>.Element` (north = 0, in clockwise order) and back — without making the bare `Compass.Cardinal` enum depend on the cyclic-group machinery.

```swift
import Compass_Cyclic_Primitives

// A compass bearing projects losslessly onto ℤ/4ℤ: north is 0, and
// clockwise order matches the group's `+1` generator.
let heading = Compass.Cardinal.north

// Rotate 90° clockwise by adding the generator in ℤ/4ℤ.
let turned = Compass.Cardinal(cyclic: heading.cyclic + .one)   // .east

// The projection round-trips for every cardinal direction.
for cardinal in Compass.Cardinal.allCases {
    assert(Compass.Cardinal(cyclic: cardinal.cyclic) == cardinal)
}
```

The projection is total in both directions — each of the four cardinals maps to exactly one group element and vice versa — so `.cyclic` and `init(cyclic:)` never fail. Importing `Compass_Cyclic_Primitives` re-exports both `Compass_Primitives` and `Cyclic_Primitives`, so `Compass.Cardinal` and `Cyclic.Group` are available without a separate import.

---

## Installation

```swift
dependencies: [
    .package(url: "https://github.com/swift-primitives/swift-compass-cyclic-primitives.git", branch: "main")
]
```

```swift
.target(
    name: "App",
    dependencies: [
        .product(name: "Compass Cyclic Primitives", package: "swift-compass-cyclic-primitives"),
    ]
)
```

Requires Swift 6.3.1 and macOS 26 / iOS 26 / tvOS 26 / watchOS 26 / visionOS 26 (or the matching Linux / Windows toolchain).

---

## Architecture

Two library products. The bridge lives here so neither `Compass_Primitives` nor `Cyclic_Primitives` has to depend on the other.

| Product | Target | Purpose |
|---------|--------|---------|
| `Compass Cyclic Primitives` | `Sources/Compass Cyclic Primitives/` | Adds `Compass.Cardinal.cyclic` and `Compass.Cardinal(cyclic:)`, the lossless projection onto `Cyclic.Group.Static<4>.Element`; re-exports `Compass_Primitives` and `Cyclic_Primitives`. |
| `Compass Cyclic Primitives Test Support` | `Tests/Support/` | Re-exports the main target for test consumers. |

Foundation-free.

---

## Platform Support

| Platform | Status |
|----------|--------|
| macOS 26 | Full support |
| Linux | Full support |
| Windows | Full support |
| iOS / tvOS / watchOS / visionOS | Supported |

---

## Community

<!-- BEGIN: discussion -->
<!-- Discussion thread created at publication. -->
<!-- END: discussion -->

## License

Apache 2.0. See [LICENSE.md](LICENSE.md).
