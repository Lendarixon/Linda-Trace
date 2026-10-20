# How updates work

Linda Trace has two independent update channels, built the same way as in the Linda detector.

## 1. Signed update list (Hugging Face)

`https://huggingface.co/Lindarixon/Linda-Trace/resolve/main/latest.json` and `latest.json.sig`.

* `latest.json` lists the **model pack** (`version`, `files[]` with `path`, `size`, `sha256`; paths are limited to `models/<name>`), the minimum app version (`min_app`) and optionally the **installer** of a newer app (`version`, `url` on GitHub Releases, `size`, `sha256`, `app_id`).
* `latest.json.sig` is a base64 Ed25519 signature over the exact bytes of `latest.json`. The public key is built into the app (`trace_config.SIGNING_PUBKEY_B64`): `1uPfXe1IO9egH/t+j0hAqzneMdtT8tmqaLSRcFnIe0E=`. The app verifies the signature before it parses the list and refuses anything else.

## 2. Model packs

The app downloads only files that are missing or changed (HTTP range resume), checks size and SHA-256, re-checks every staged file, then replaces the installed files atomically and records the signed manifest as the installed marker. If anything fails, the previous files are restored. A model pack that is not newer than the installed one is refused. Downloaded packs live in `%LOCALAPPDATA%\ForensicAuthorship\trace_update`; if a file there is damaged the app silently falls back to the model bundled with the installer. Each analysis records which model pack produced it.

## 3. Application updates

When the signed list names a newer installer, the app downloads it from GitHub Releases, checks SHA-256 and size, keeps the signed manifest next to it, and verifies everything again just before launching. It then closes itself, runs the installer silently (`/SILENT /CLOSEAPPLICATIONS`) after the process has exited, and the installer starts the new version.

The installer is not code-signed yet; the SHA-256 in the signed list protects the update channel.

## Turning it off

The Updates window has a *Check for updates automatically* switch. With it off the app contacts the network only when you press *Check for updates*.
