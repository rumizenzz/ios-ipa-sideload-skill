# ios-ipa-sideload (Codex Skill)

This repository contains the **Codex skill** `ios-ipa-sideload`.

## What it does

Autonomously sideloads iOS apps (`.ipa`) onto an iPhone or iPad with a guided workflow (Sideloadly + on-device trust steps).

## Requirements

- Codex installed (IDE extension on Windows/macOS, or Codex app on macOS)
- Signed in
- Run Codex once (so it creates your Codex folder on disk)

Note: The Codex app is currently macOS-only. Windows users should use the Codex IDE extension.

## Install (manual)

This repo ships the skill at:

- `ios-ipa-sideload/`

Copy it into your Codex skills folder:

- macOS:

```bash
CODEX_HOME="${CODEX_HOME:-$HOME/.codex}"
mkdir -p "$CODEX_HOME/skills"
cp -R "ios-ipa-sideload" "$CODEX_HOME/skills/"
```

- Windows (PowerShell):

```powershell
$codexHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE ".codex" }
New-Item -ItemType Directory -Force -Path (Join-Path $codexHome "skills") | Out-Null
Copy-Item -Recurse -Force -Path "ios-ipa-sideload" -Destination (Join-Path (Join-Path $codexHome "skills") "ios-ipa-sideload")
```

Then restart Codex.

## Use

In Codex, run:

`/ios-ipa-sideload`
