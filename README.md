# yubikey-listener

Desktop notifier for [yubikey-touch-detector](https://github.com/maximbaz/yubikey-touch-detector) events.

When your YubiKey is waiting for a touch, a critical notification appears showing which tool triggered the request (e.g. `pass decrypt: ~/.password-store/GH_TOKEN`, `git push: git@github.com/...`, `ssh authenticate: github.com`). The notification dismisses itself automatically once the touch is complete.

## Requirements

- [yubikey-touch-detector](https://github.com/maximbaz/yubikey-touch-detector) running and emitting D-Bus signals
- A notification daemon (e.g. `dunst`, `mako`, `swaync`)

## Installation

**Nix flake:**
```
nix profile install github:talgarr/yubikey-listener
```

**From source:**
```
go install github.com/talgarr/yubikey-notifier@latest
```

## Usage

```
yubikey-listener [--verbose]
```

Run it as part of your desktop session. With systemd:

```ini
[Unit]
Description=YubiKey touch notifier
After=graphical-session.target

[Service]
ExecStart=%h/go/bin/yubikey-listener
Restart=on-failure

[Install]
WantedBy=graphical-session.target
```

## Supported tools

| Tool | Detected operations |
|------|-------------------|
| `pass` | show, insert, generate, edit |
| `sops` | encrypt, decrypt, edit, rotate |
| `age` / `rage` | encrypt, decrypt |
| `git` | push, pull, fetch, clone, signed commit |
| `gpg` / `gpg2` | sign, decrypt, encrypt, verify |
| `ssh` / `scp` / `sftp` | authenticate |
| browsers | WebAuthn / passkey |

When the calling process isn't recognised, the raw process chain is shown instead.

## License

MIT
