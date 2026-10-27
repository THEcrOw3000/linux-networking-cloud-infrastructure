# Linux, Networking & Cloud Infrastructure

## Project overview
This project documents a practical Linux deployment lab covering:
1. Linux environment setup and system inspection
2. Networking basics and secure access
3. Web service deployment with Nginx
4. Connectivity checks and troubleshooting

## Environment
For a no-cost learning environment, this lab can be run in a personal GitHub Codespace (subject to the included monthly quota). Codespaces is a cloud-hosted development environment, not a permanently running standalone cloud VM such as AWS EC2. Record the actual environment used in your evidence.

## Lab workflow
- [ ] Create/open a personal GitHub Codespace for this repository.
- [ ] Run the commands in `docs/linux-commands.md`.
- [ ] Review `docs/networking-and-security.md`.
- [ ] Run `scripts/server-setup.sh` if the environment supports `sudo` and `apt`.
- [ ] Run the verification commands in `docs/deployment-evidence.md`.
- [ ] Save genuine screenshots in `screenshots/`.
- [ ] Update the results section below with what you actually observed.

## Results (complete after running)
- Environment used: TODO
- Linux distribution/version: TODO
- Nginx service status: TODO
- HTTP test result: TODO
- SSH test result (if performed): TODO
- Issues and fixes: TODO

## Important notes
- Do not commit private SSH keys, passwords, tokens, or other secrets.
- Do not claim a command succeeded until you have run it and observed the result.
- In Codespaces, the forwarded web port may be private by default. Use the Ports panel to open or share it only as appropriate.
- A Codespace is subject to usage quotas and can stop when idle.

## Repository structure
- `docs/` — setup, networking, security, and verification notes
- `scripts/server-setup.sh` — basic Ubuntu/Debian setup helper
- `screenshots/README.md` — evidence checklist
