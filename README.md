# bloom-poni
I built the combined repo at /root/bloom-poni, but I couldn't push it. Creating DrS373n/bloom-poni failed with "Resource not accessible by integration", so this session isn't authorized to create repos. To publish it, create the empty repo yourself, then run:

Code
cd /root/bloom-poni && git remote add origin <url> && git push -u origin main
What's in it (one commit):

Layout: bloom/ and oyenza-studio/ (which contains Poni) sit side by side. I didn't carry over either repo's git history.
Island removed: I deleted Bloom's island UI (App.tsx, CompactMediaPlayer.tsx). The frontend builds cleanly with vite build, and tsc reports no errors.
Dock kept: the dock, settings and overlay are untouched.
Poni added: a new bloom/src-tauri/src/poni.rs starts poni.exe when Bloom launches and stops it on exit. tauri.conf.json bundles oyenza-studio/target/release/poni.exe, and the root README.md has the build steps.
Not verified:

Rust and Windows: I haven't compiled the Rust or tested anything on Windows, since this environment isn't Windows. Build Poni with cargo build --release -p poni first so the bundle step finds poni.exe.
Hidden "main" window: Bloom's Rust backend still manages its old "main" window in many places, so I kept it as an empty hidden window rather than ripping those references out.