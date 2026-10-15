# Zenkai Clay personal macOS build

Run **Zenkai Clay for Apple Silicon** from the Actions tab. The workflow targets
ARM64 Macs, including the M4, on standard `macos-26` GitHub-hosted runners. Xcode
is installed on the runner; it is not required on the Mac that runs the app.

The `helium-chromium` submodule points to the Zenkai Clay commit in
`Glvent/helium`. The preset is built into Settings → Appearance. Selecting it
switches to its dark palette; it does not change the default theme for existing
profiles.

The first build may take roughly 12–36 hours on the standard runner. This is an
estimate, not a measured result. The existing Helium workflow saves a checkpoint
after about five hours and resumes on another runner, for up to ten build
phases. Download the completed DMG artifact from the workflow run once all jobs
are green. The last job verifies its SHA-256 checksum, ad-hoc signature, ARM64
architecture, and headless startup and rendering.

No Apple Developer credentials or upstream release secrets are required. The
app is ad-hoc signed, not notarized. If macOS blocks the downloaded app, use
System Settings → Privacy & Security → Open Anyway after trying to open it.
Keep a backup of an existing Helium app before replacing it, and close Helium
before installation. Browser data is not part of the DMG.

The workflow does not publish releases or enable the Sparkle updater. The DMG
expires after seven days; temporary source and checkpoint artifacts expire
after three days and one day respectively, and are deleted after verification.
Standard runner compute is free for public repositories. GitHub's account
storage rules still apply; no spending limits or repository protections are
changed by this workflow.

If a phase fails, inspect its logs and use **Re-run failed jobs** while its input
artifacts remain available. After they expire, start a new workflow run. If all
ten phases finish without producing a DMG, verification fails instead of
reporting a successful build.
