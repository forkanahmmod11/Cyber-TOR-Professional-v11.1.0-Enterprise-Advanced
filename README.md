
## v11.0.0 Enterprise Intelligence Upgrade

See `ENTERPRISE-UPGRADE-11.md` for the new enterprise asset inventory, vulnerability correlation, dynamic risk engine, evidence sealing, secret/container security, compliance matrix, scheduling registry and Security Center capabilities.

## Enterprise Capability Profile

See `ENTERPRISE-CAPABILITIES.md` for the v10.0 assessment architecture, evidence model, governance layer and international productization roadmap.

# CYBER TOR PROFESSIONAL v11.0.0

**Enterprise Cybersecurity Assessment, Exposure Management, Risk Intelligence & Defensive Security Platform**

Cyber Tor Professional is a local, scope-controlled platform for authorized security assessment, defensive file analysis, integrity monitoring, ransomware-activity detection, evidence collection, reporting, and controlled infrastructure credential management.

## v10.0.0 control-plane improvements

- Mandatory HTTPS registration for managed websites
- Explicit hostname/IP/CIDR/wildcard scope validation
- Per-site connector tokens stored only as SHA-256 hashes
- One-time connector token display and immediate token rotation
- Authenticated connector status, heartbeat and event API
- AES-256-GCM encrypted infrastructure vault with random master key
- PBKDF2-HMAC-SHA256 password-based master-key wrapping
- Existing secrets are never rendered back to the browser
- CSRF protection on administrative state-changing forms
- Atomic vault/configuration writes
- Administrative and connector audit log
- No arbitrary remote command execution exposed by the control plane


## v10.0 Deep Web Pentest Engine

- Bounded same-origin crawling with explicit scope re-validation
- Endpoint and form discovery without form submission
- Safe active endpoint validation
- Authentication/session security observations
- REST/API/OpenAPI/Swagger/GraphQL surface discovery
- HTTP method posture validation
- Verbose-error and server-error detection
- Evidence-backed findings with confidence and location
- Deep Web and Enterprise pentest profiles
- Destructive exploitation, credential attacks, persistence and out-of-scope requests are intentionally disabled

## Assessment capabilities

- Web security posture and configuration auditing
- Adaptive technology / stack intelligence
- TLS, DNS, certificate and network-service assessment
- API, CORS, cookie, JavaScript and HTTP-method audits
- Cloud/WAF/CDN exposure checks
- Authentication and endpoint discovery checks
- Subdomain and dependency/version intelligence
- Nmap integration with scope enforcement
- Evidence-weighted risk scoring
- JSON evidence reports and consolidated HTML audit reports
- Local anti-malware indicator analysis and optional quarantine
- Integrity baselines and ransomware-activity guard
- Kali Linux, Ubuntu and Termux friendly

## Infrastructure Access Vault

For each explicitly authorized site, the local panel can securely store hosting provider metadata, hosting/DNS API tokens, SSH/SFTP credentials, database connection metadata and operator notes. Secrets are encrypted at rest and are not displayed after storage. The product does not provide unrestricted remote shell execution; provider-specific operational adapters can be added as separately scoped integrations.

## Local administration

Run:

`./cyber-tor admin`

The first run creates an administrator account. The dashboard binds to `127.0.0.1` by default. For remote administration, use a trusted TLS reverse proxy/VPN and network ACLs.

## Connector

The included `site_connector.py` supports:

- `status` — read connector/site state
- `heartbeat` — publish connector liveness
- `event` — publish a short authorized audit/health event

Example:

```bash
python3 site_connector.py --panel http://127.0.0.1:8787 --site-id SITE_ID --token CONNECTOR_TOKEN heartbeat
```

## Installation

```bash
./install.sh
./cyber-tor --help
```

Termux:

```bash
./install-termux.sh
./cyber-tor --help
```

## Testing

```bash
python3 -m unittest discover -s tests -v
```

## Safe operation

Use network modules only against systems you own or are explicitly authorized to assess. High-impact exploitation, credential attacks and destructive actions are intentionally outside the product's design.

## v10.0 Infrastructure Operations

The v10.0 control plane includes scope-controlled, read-only infrastructure adapters:

- `cloudflare_dns` — DNS zone/record inventory using a scoped Cloudflare API token.
- `cpanel_hosting` — HTTPS-only cPanel server health/information query using an API token.
- `local_backup` — local encrypted-state archive snapshots; credentials remain encrypted inside the vault.

No adapter exposes arbitrary SSH/shell execution, remote file upload, DNS mutation, or destructive infrastructure actions.

Configure provider credentials from **Websites → Infrastructure Access Vault**, then use **Operations** for the authorized site.
## Project layout and startup

The executable launcher is `./cyber-tor`; the Python application entry point is `src/cyber_tor.py`. Runtime state and reports are stored under the project-root `state/` and `reports/` directories.

```bash
chmod +x cyber-tor
./cyber-tor
```

## Web Control Panel

Start the application with `./cyber-tor` and open `http://127.0.0.1:8787/`. The authenticated Security Assessment Center invokes `src/cyber_tor.py` with the global `--scope` option in the correct argument order.

## Enterprise IAM (v11.0)

Multi-user RBAC, TOTP MFA enrollment/verification, account enable/disable, MFA reset, scoped connector API permissions, password hashing, session controls and audit logging are available in the local control plane. See `ENTERPRISE-AUTH.md`.

## v11.1 Enterprise Platform Upgrade

- Vulnerability lifecycle with CVSS v4/EPSS fields and remediation verification
- Safe attack-surface snapshots with DNS discovery and change tracking
- Offline cloud inventory/configuration posture audit
- Threat-intelligence IOC import/lookup
- Remediation queue and overdue SLA visibility
- Enterprise Security Center platform metrics
- See `ENTERPRISE-PLATFORM-11.1.md`
