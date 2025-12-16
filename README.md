# Cross-Platform Nginx SSL Proxy Automation

This Ansible playbook automatically sets up nginx SSL proxies with mkcert certificates for local development on both Linux and macOS.

## Quick Start

```bash
# Run the automation
ansible-playbook -i inventory/hosts site.yml -e "magazine=your-domain.magsquare.com"
```

## Configuration

### Main Variables (`vars/main.yml`)
- `magazine`: Your magazine domain (required)
- `base_domains`: Base HTTPS domains
- `backends`: Upstream service URLs

### Platform Variables (`vars/platform.yml`)
Auto-detects platform and sets:
- Package manager (apt/homebrew)
- Certificate directory
- Nginx config paths
- Binary locations

## Supported Platforms
- **Linux**: Ubuntu/Debian with apt
- **macOS**: With Homebrew

## What It Does
1. Installs mkcert and nginx
2. Generates SSL certificates for all domains
3. Configures nginx SSL proxies for:
   - Dashboard (dashboard.local)
   - API (api.magsquare.com, api.{magazine})
   - Reader ({magazine})
   - Keycloak (localhost:8443)
4. Updates /etc/hosts entries

## Services Proxied
- Dashboard: https://dashboard.local → http://127.0.0.1:5173
- API: https://api.magsquare.com → http://127.0.0.1:8000
- Reader: https://{magazine} → http://127.0.0.1:81
- Keycloak: https://localhost:8443 → http://127.0.0.1:8080