# craftkit

Write Minecraft mods in Rust.

craftkit has two halves, both here:

- **`sdk/`, the `craftkit` crate:** what a mod is written against. A mod implements the `Mod`
  trait, exports it with `export_mod!`, and is built as a shared library. It never touches
  Minecraft's classes: once a tick it is handed what the world did and answers with what it
  wants done, so it is tested with the crate's harness in plain `cargo test`. See the
  [crate's README](sdk/README.md) for a whole mod.
- **`host/`, the craftkit host:** a Java mod for Fabric and NeoForge that loads craftkit mods
  through Java's FFM API, hands them the world and carries out their commands. Players need it
  in the game beside a craftkit mod, or nested inside the mod's own jar.

Minecraft Java 26.3 on Java 25, with Fabric or NeoForge. The [SDK guide](docs/sdk.md) describes
the protocol, the C ABI and what the host does.

## Building

```sh
cargo test                     # the crate, its harness and its doctests
cd host && ./gradlew build     # the host jars (host/fabric/build/libs, host/neoforge/build/libs) and their tests
```

## Where it is developed

craftkit is developed in [lodger](https://github.com/germ3n/lodger), its first mod, so the two change together;
this repository is exported from there (`scripts/export_craftkit.py`). Issues and pull requests
are welcome here.

## License

MIT.
