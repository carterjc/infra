# platform

## access

Komodo is only accessible on the internal network. For reference,

- `http://10.0.0.51:9120/`: Komodo (`carter` and `admin` accounts)
- `http://10.0.0.51:5000/`: Dockflare

Also, the Proxmox VM's console login isn't configured, so use ssh instead (user: `carter`).

## notes

Using Komodo's ferretdb offering because my Proxmox server can't run MongoDB 5.

```WARNING: MongoDB 5.0+ requires a CPU with AVX support, and your current system does not appear to have that!```

---

Periphery servers are not using systemd so can't natively access fs - there's a custom mount in [the Komodo compose file](/platform/komodo/ferretdb.compose.yml) to circumvent this.

## Komodo commands

```bash
# up
docker compose -p komodo -f ferretdb.compose.yml --env-file compose.env up -d
# down
docker compose -p komodo -f ferretdb.compose.yml --env-file compose.env down
```
