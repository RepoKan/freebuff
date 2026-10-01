# Run Codebuff from GitHub instead of iSH

## Why this path exists

iSH exposes a 32-bit Linux x86 environment (`ia32` / `i686`). The current Codebuff binary build only declares Linux targets for `x64` and `arm64`, so rebuilding the same binary inside iSH does not remove the architecture mismatch.

This repository can instead run Codebuff in a GitHub Codespace, where the CLI runs on a supported Linux x64 host while the iPhone is only the client UI.

## Start a Codespace

1. Open this repository on GitHub.
2. Select **Code -> Codespaces**.
3. Create a Codespace from branch `github-codebuff-ish`.
4. Wait for the devcontainer setup to finish.

The devcontainer installs Node 22 and Bun 1.3.14, then restores the monorepo dependencies with the committed lockfile.

## Run Codebuff from source

In the Codespace terminal:

```bash
bun --version
node --version
uname -m
bun start-cli
```

Expected architecture:

```text
x86_64
```

`bun start-cli` launches the Codebuff CLI from the monorepo source.

## Build a standalone Linux x64 Codebuff binary

From the repository root:

```bash
bun --cwd cli run build:binary
./cli/bin/codebuff --version
```

The build also places `tree-sitter.wasm` next to the binary.

## Important

The resulting Linux x64 binary is for the GitHub/Codespaces host or another x64 Linux machine. It is not an iSH-native binary and should not be copied back to iSH expecting it to execute there.

Use iSH for lightweight shell work and Git, and use the GitHub Codespace for Codebuff itself.
