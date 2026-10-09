# Portable Codex setup

This repository contains a portable set of Codex instructions and skills for
development, research, Flutter/Dart work, voice/audio processing, and Wiki-based
project context.

The package is designed for Windows, macOS, and Linux. Do not copy the current
machine-specific `codex/config.toml` or `codex/hooks.json` blindly: they may contain
absolute paths for the original computer. Use the templates and replace paths for
the target machine.

## 1. Prerequisites

Required:

- Codex with skills support;
- Git.

Optional:

- Python 3.10+ for Z.A.E.B.A.L.; Python 3.13+ is recommended;
- Flutter SDK and Dart SDK for Flutter/Dart MCP;
- Obsidian, if you want to use the LLM Wiki.

## 2. Choose the LLM Wiki path

During installation, ask the user for the local path to the Wiki. Do not assume
`H:\LLM-WIKI`: that path belongs to the original Windows machine.

Examples:

- Windows: `H:\LLM-WIKI`
- macOS: `/Users/<user>/Documents/LLM-WIKI`
- Linux: `/home/<user>/Documents/LLM-WIKI`

Replace `<LLM_WIKI_PATH>` in `codex/AGENTS.md.template` with the selected path.
If the user does not use an LLM Wiki, remove or disable the Wiki section instead
of inventing a path.

## 3. Install skills

Copy the directories under `skills/` into the user's global Codex skills folder:

- Windows: `%USERPROFILE%\\.codex\\skills`
- macOS/Linux: `~/.codex/skills`

Keep the existing `.system` directory. Copy only the portable skill directories.
Restart Codex after installation.

## 4. Install global instructions

Copy `codex/AGENTS.md.template` to the global Codex location:

- Windows: `%USERPROFILE%\\.codex\\AGENTS.md`
- macOS/Linux: `~/.codex/AGENTS.md`

Before copying, replace `<LLM_WIKI_PATH>` and review the local language and project
conventions.

## 5. Configure Flutter/Dart MCP

Make sure `dart` is available in PATH:

```text
dart --version
```

Then add this to the user's Codex `config.toml`:

```toml
[mcp_servers.dart]
command = "dart"
args = ["mcp-server"]
startup_timeout_sec = 120
```

If `dart` is not in PATH, use the absolute path to the SDK executable. For a
Flutter installation, it is commonly under:

```text
<flutter-sdk>/bin/cache/dart-sdk/bin/dart.exe   # Windows
<flutter-sdk>/bin/cache/dart-sdk/bin/dart       # macOS/Linux
```

Restart Codex and ask it to list the available Dart/Flutter MCP tools. Runtime
inspection requires a running Flutter application connected to the SDK.

## 6. Configure Z.A.E.B.A.L. (optional)

Install Python 3.10 or newer and verify it:

```text
python --version
```

Use the Z.A.E.B.A.L. repository matching the installed `skills/zaebal` version.
Install only the hook for the host and operating system actually in use. Do not
install Linux hooks on Windows or enable unsafe external auditors by default.

If Python or host hook integration is unavailable, the `zaebal` skill can still
be installed and used manually.

## 7. Verify

Check:

1. Codex sees the installed skills after restart.
2. The Wiki path exists, if configured.
3. `dart --version` works, if Flutter MCP is configured.
4. Codex can list the Dart/Flutter MCP tools.
5. A normal prompt does not trigger Z.A.E.B.A.L.

## Security and privacy

Never publish these files:

- `auth.json`;
- API keys, tokens, passwords, `.env` files;
- session history, logs, memories, or internal SQLite databases;
- private Wiki contents;
- machine-specific credentials or absolute paths that reveal private infrastructure.

Review every third-party skill before enabling it. Skills are instructions and may
include scripts that run on the user's machine.
