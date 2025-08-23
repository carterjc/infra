# homelab infra

GitOps repo to manage homelab hardware in an attempt to slowly make things more declarative (no more random one-shot LXCs/VMs on Proxmox).

Using [Komodo](https://komo.do) as a thin wrapper around Docker. This infra is running on my Proxmox server in a Debian VM (config in [/cloudinit/](/cloudinit/))- little bit odd, but since I use my Proxmox server for test VMs and the such, having the hypervisor still makes sense.

## roadmap

Don't want to add more services than I need, and am pretty happy with how it is right now. The next big things are

- Automating deployments for personal apps, like Joyce
- Backing up data (particularly Joyce's application data) using Komodo actions, potentially + figuring out where to back it up (I'm just always scared about Docker's ephemerality)
- Maybe spending more time managing the komodo.toml file and configuring the Resource Sync
