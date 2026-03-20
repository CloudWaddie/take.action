# 🔬 take.action | Serverless RE-Analyzer

[![GitHub Actions Status](https://github.com/cloudwaddie/take.action/workflows/Reverse%20Engineer%20Analyser/badge.svg)](https://github.com/cloudwaddie/take.action/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A fully automated, serverless malware triage and reverse engineering pipeline built entirely on GitHub Actions. 

Drop a suspicious binary into the repository, and GitHub will spin up an ephemeral clean-room environment, analyze the file, extract hidden capabilities, and perform the heavy CPU lifting of Ghidra Auto-Analysis. It then bundles the intelligence reports and the pre-computed Ghidra project into a neat ZIP file. 

## ⚙️ The Tool Stack

* **[Magika](https://google.github.io/magika/)**: AI-powered, deep-learning file identification.
* **[Detect-It-Easy (DIE)](https://github.com/horsicq/Detect-It-Easy)**: Advanced packer, compiler, and signature detection.
* **[Capa](https://github.com/mandiant/capa)**: Behavioral capability mapping.
* **[FLOSS](https://github.com/mandiant/flare-floss)**: FireEye Labs Obfuscated String Solver (extracts hidden C2 domains).
* **[Rizin](https://rizin.re/)**: High-speed extraction of imports, exports, and binary headers.
* **[Ghidra (Headless)](https://ghidra-re.org/)**: Offloads Auto-Analysis to the cloud, generating a ready-to-open `.gpr` database.

## 🚀 How It Works

1. **Upload:** Push a new executable or packed binary to the `binaries/` folder.
2. **Trigger:** The GitHub Action detects the new file and spins up an Ubuntu runner.
3. **Analyze:** The runner installs the tools and executes them strictly on the newly added files.
4. **Compile:** Ghidra runs headlessly, performing full auto-analysis to save your local CPU from the heavy lifting.
5. **Archive & Alert:** The text reports and the Ghidra `.gpr` project are zipped, uploaded as an Action Artifact, and an alert is sent to a configured Discord channel.

## 📂 Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── re-analyzer.yml    # The core GitHub Actions pipeline
├── binaries/                  # 📥 DROP MALWARE/BINARIES HERE
└── README.md
