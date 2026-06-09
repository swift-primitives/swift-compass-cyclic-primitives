# swift-compass-cyclic-primitives

The lossless projection between `Compass.Cardinal` and the cyclic group `Cyclic.Group.Static<4>`
(Z/4Z) — a per-carrier bridge ([MOD-014]) adding `.cyclic` and `init(cyclic:)` so the bare
`Compass.Cardinal` enum carries no cyclic-group dependency. Clockwise rotation is `+1` in Z/4Z.

```swift
import Compass_Cyclic_Primitives

Compass.Cardinal.north.cyclic                          // Z/4Z element 0
Compass.Cardinal(cyclic: Compass.Cardinal.north.cyclic + .one)  // .east
```

## License

Apache License 2.0. See [LICENSE](LICENSE.md).
