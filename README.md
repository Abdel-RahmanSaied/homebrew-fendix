# homebrew-fendix

Public install mirror for **Fendix** — a hybrid API and code security scanner.

Fendix combines live HTTP probing (Go) with static code analysis (Python) to find auth bypasses, injection flaws, exposed secrets, and dependency CVEs. When both engines agree on a vulnerability, it surfaces as a *correlated* finding with elevated confidence.

This repository hosts the install scripts, Homebrew formula, and pre-built release binaries. The engine source lives in a private repository during development; only build artifacts and install tooling are public here.

## Install

### Homebrew (macOS / Linux)

```bash
brew tap Abdel-RahmanSaied/fendix
brew install fendix
```

### curl pipe (macOS / Linux)

```bash
curl -fsSL https://raw.githubusercontent.com/Abdel-RahmanSaied/homebrew-fendix/main/install.sh | sh
```

Downloads the latest release binary, verifies its sha256 checksum, and installs to `/usr/local/bin/fendix`. Override the install dir with `FENDIX_DIR=$HOME/.local/bin` or pin a version with `FENDIX_VERSION=v0.4.0`.

### Docker

```bash
docker pull ghcr.io/abdel-rahmansaied/fendix:latest
docker run --rm ghcr.io/abdel-rahmansaied/fendix scan --url https://api.example.com
```

The Docker image includes Python and all static analysis dependencies, so hybrid mode works out of the box.

### Manual download

Pick a binary for your platform from the [latest release](https://github.com/Abdel-RahmanSaied/homebrew-fendix/releases/latest) (linux/amd64, darwin/amd64, darwin/arm64), verify its `.sha256` sidecar, and place it on your PATH:

```bash
curl -fsSL -o fendix https://github.com/Abdel-RahmanSaied/homebrew-fendix/releases/download/v0.4.0/fendix-v0.4.0-darwin-arm64
shasum -a 256 fendix  # compare against the .sha256 file alongside the binary
chmod +x fendix && sudo mv fendix /usr/local/bin/fendix
```

## Verify

```bash
fendix version
fendix scan --url https://httpbin.org --format html --output report.html
```

## Releases

Releases are produced from the private engine repository and mirrored here automatically on every `v*` tag. Each release includes:

- `fendix-vX.Y.Z-linux-amd64` + `.sha256`
- `fendix-vX.Y.Z-darwin-amd64` + `.sha256`
- `fendix-vX.Y.Z-darwin-arm64` + `.sha256`

`linux/arm64`, signed binaries, and `.deb`/`.rpm` packages are planned for v1.0.

## License

MIT — see [LICENSE](LICENSE).
