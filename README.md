# firefox-vpn-client

A small Go-based VPN client intended to work with Firefox VPN services and developer workflows.

This repository is primarily implemented in Go (≈90%) with some shell scripts (≈10%).

## Features

- Native Go implementation for a small footprint client
- Simple command-line interface for connecting and disconnecting
- Example scripts for common platforms (Linux/macOS)

> Note: This README is based on the repository name and language composition. If you provide additional project details (protocol, required server, credentials format, config file path), I can extend these docs with exact usage examples.

## Requirements

- Go 1.20+ (or latest stable Go) installed
- Root/Administrator privileges to configure TUN/TAP or routing on some platforms

## Build

Clone the repository and build with go:

```bash
git clone https://github.com/haliyari/firefox-vpn-client.git
cd firefox-vpn-client
# build
go build -o firefox-vpn-client ./...
```

Or use `go install`:

```bash
go install github.com/haliyari/firefox-vpn-client@latest
```

## Usage

Usage depends on the CLI the repository provides. The common patterns are shown below — replace flags with the real ones if they differ:

```bash
# show help
./firefox-vpn-client --help

# connect to VPN (example)
sudo ./firefox-vpn-client connect --server vpn.example.com --token $TOKEN

# disconnect
sudo ./firefox-vpn-client disconnect
```

If the project expects a config file, look for `config.yaml`, `config.json`, or a path described in the code (commonly `~/.config/firefox-vpn-client/` or `/etc/firefox-vpn-client/`).

## Example systemd unit (Linux)

If you want the client to run as a system service, create `/etc/systemd/system/firefox-vpn-client.service`:

```ini
[Unit]
Description=Firefox VPN Client
After=network-online.target

[Service]
Type=simple
ExecStart=/usr/local/bin/firefox-vpn-client connect --config /etc/firefox-vpn-client/config.yaml
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

Then:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now firefox-vpn-client.service
```

## Development

- Format code: `gofmt -w .`
- Run tests (if present): `go test ./...`
- Linting: use `golangci-lint` or another linter

## Contributing

Contributions are welcome. Please open issues or pull requests describing the change. Follow these guidelines:

- Open an issue first for large features
- Keep commits small and focused
- Write tests for new behavior where possible

## Troubleshooting

- Permission issues: ensure you have the required capabilities to manipulate network interfaces (CAP_NET_ADMIN on Linux) or run with `sudo`.
- Build failures: verify your Go version and module download access (proxy/firewall).

## License

If this project is intended to be open source, add a LICENSE file (MIT, Apache-2.0, etc.).

## Contact

Created by @haliyari. If you'd like this README tailored (add real CLI usage, config format, or examples), share the expected flags or point to the relevant source files and I will update it.
