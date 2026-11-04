# Bloom + Oyenza Studio

A Windows desktop app combining Bloom's taskbar-replacement dock with Oyenza
Studio's Poni island. Bloom's hidden main window remains as the dock's
background bootstrap; the visible island is provided by Poni.

## Build on Windows

Use Windows 10/11 with the Rust MSVC toolchain, Visual Studio C++ build tools,
Bun 1.4.0, and the WebView2 runtime.

```powershell
cd oyenza-studio
cargo build --locked --release --package poni --target x86_64-pc-windows-msvc

cd ../bloom
bun install --frozen-lockfile
bun run tauri build --bundles nsis
```

The NSIS installer is written under
`bloom/src-tauri/target/release/bundle/nsis/`. It includes `poni.exe`, so a
separate Oyenza installation is not needed.

## Releases

The root GitHub Actions release workflow builds Poni, bundles it with Bloom,
and publishes the Windows NSIS `.exe` installer when a `v*` tag is pushed.
Before tagging, commit the app changes and configure the repository secrets
`TAURI_SIGNING_PRIVATE_KEY` and `TAURI_SIGNING_PASSWORD` to match the updater
public key in `bloom/src-tauri/tauri.conf.json`.

From `bloom/`, run `bun run release <major.minor.patch>` on `main` to bump the
Bloom version, create and push its release tag, and start the workflow.
