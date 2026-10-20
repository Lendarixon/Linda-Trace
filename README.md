<p align="center"><img src="app-icon.png" alt="Linda Trace" width="96"></p>

# Linda Trace

**A local text investigator for Windows.** Compare the writing style of documents and see which texts differ from the rest, or check questioned texts against samples of known authors. English, Russian and Polish. Everything runs on your PC: your texts are never uploaded.

- Website: https://lendarixon.github.io/Linda-Trace/ (English, Russian, Polish)
- Download: [Releases](https://github.com/Lendarixon/Linda-Trace/releases) - `LindaTrace-1.0.0-Setup.exe` (Windows 10/11 x64, per-user install, no administrator rights)
- Model pack and signed update list: https://huggingface.co/Lindarixon/Linda-Trace
- By the author of [Linda, the local AI-text detector](https://lendarixon.github.io/Linda/)

## What it does

| Mode | Input | Output |
|---|---|---|
| Compare documents | 4-200 documents in one language, at least 300 words each (about 1,000 is better) | ranking by how much each differs in style from the others, the features behind it, the most different 300-word fragments, a 2D style map |
| Check authorship | questioned texts + samples of known authors (at least 2 samples per author, at least 2 authors) | nearest candidate authors by style - candidates, not probabilities |

Formats: TXT, DOCX, PDF, RTF, HTML, Markdown. Exports: HTML, PDF, JSON, ZIP archive with file hashes. Saved datasets stay on the PC. Light, dark and high-contrast themes; interface in Russian, English and Polish.

## Updates

The **Updates** button in the app header checks a signed update list (`latest.json` + `latest.json.sig`, Ed25519) on Hugging Face. Model packs are downloaded, SHA-256 checked and applied atomically (the previous pack is restored if anything fails); application updates come from the GitHub Releases of this repository, are verified by signature and SHA-256, installed silently, and the app restarts. The automatic check at start can be switched off in the Updates window. Only the update list and update files are downloaded; texts and documents are never sent. Details: [UPDATES.md](UPDATES.md).

## What the results mean

Results are relative style distances inside the corpus you supply. They do not prove authorship, identity, authenticity or leaks and do not replace expert examination. Short texts (under 300 words), lists, forms and slides are unreliable; character n-grams can reflect topic or source as well as the author.

Evidence, exactly: on an independent held-out test of 92 historical literary works (authors who died 1852-1925) top-1 accuracy of the shipped fused ranking was 9/17 English, 9/19 Polish and 14/24 Russian (the plain n-gram score alone: 12/17, 12/19, 14/24). On modern institutional prose (US Supreme Court opinions 2024-2025, 5 justices x 4 opinions) top-1 was 4/10 for all methods, so modern and corporate texts are **not** covered by any claim. The samples are small - run your own checks.

## Install

Download the installer from Releases and run it. The installer is not code-signed yet, so Windows SmartScreen may warn: choose *More info*, then *Run anyway*, and compare the SHA-256 published with the release (`SHA256SUMS.txt`). Data is stored in `%LOCALAPPDATA%\ForensicAuthorship`; uninstalling asks whether to delete it.

## License

Proprietary build, copyright 2026 project owner, all rights reserved. Use is under a separate agreement with the owner; you are responsible for the rights to the documents you analyse. See [LICENSE.txt](LICENSE.txt). Third-party component notices ship inside the app (`THIRD_PARTY_NOTICES`).

Questions and bug reports: [GitHub Issues](https://github.com/Lendarixon/Linda-Trace/issues).
