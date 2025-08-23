# platform

Using Komodo's ferretdb offering because my Proxmox server can't run MongoDB 5

`WARNING: MongoDB 5.0+ requires a CPU with AVX support, and your current system does not appear to have that!`

## access

Komodo is only accessible on the internal network. For reference,

- `http://10.0.0.59:9120/`: Komodo (`carter` and `admin` accounts)
- `http://10.0.0.59:5000/`: Dockflare

Also, the Proxmox VM's console login isn't configured, so use ssh instead (user: `carter`).
