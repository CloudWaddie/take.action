# 🔬 take.action | Serverless RE-Analyzer

[![GitHub Actions Status](https://github.com/cloudwaddie/take.action/workflows/Reverse%20Engineer%20Analyser/badge.svg)](https://github.com/cloudwaddie/take.action/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A fully automated, serverless malware triage and reverse engineering pipeline built entirely on GitHub Actions. 

Drop a suspicious binary into the repository, and GitHub will spin up an ephemeral clean-room environment, analyze the file using industry-standard tools, extract hidden capabilities, and bundle the intelligence reports into a neat ZIP file. Notifications are automatically pushed to Discord via Webhooks.

## ⚙️ The Tool Stack

This pipeline dynamically fetches and utilizes a stack of command-line reverse engineering tools:

* **[Magika](https://google.github.io/magika/)**: AI-powered, deep-learning file identification.
* **[Detect-It-Easy (DIE)](https://github.com/horsicq/Detect-It-Easy)**: Advanced packer, compiler, and signature detection (Dynamically pulled via GitHub API).
* **[Capa](https://github.com/mandiant/capa)**: Behavioral capability mapping (identifies what the malware *can* do without running it).
* **[FLOSS](https://github.com/mandiant/flare-floss)**: FireEye Labs Obfuscated String Solver (extracts hidden C2 domains and API keys).
* **[Rizin](https://rizin.re/)**: High-speed extraction of imports, exports, and binary headers.
* **[Ghidra (Headless)](https://ghidra-re.org/)**: Automated static analysis and C pseudo-code generation.

## 🚀 How It Works

1. **Upload:** Push a new executable or packed binary to the `binaries/` folder.
2. **Trigger:** The GitHub Action detects the new file and spins up an Ubuntu runner.
3. **Analyze:** The runner installs the tool stack and executes the analysis strictly on the newly added files.
4. **Report:** The raw output from each tool is saved into a dedicated folder (e.g., `reports/sample-exe/`).
5. **Archive & Alert:** The results are zipped, uploaded as an Action Artifact, and an alert is sent to a configured Discord channel. The runner is then destroyed, leaving zero local footprint.

## 📂 Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── re-analyzer.yml    # The core GitHub Actions pipeline
├── binaries/                  # 📥 DROP MALWARE/BINARIES HERE
└── README.md
