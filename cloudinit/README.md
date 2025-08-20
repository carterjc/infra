# cloud init setup

Debian cloudinit image: `https://cloud.debian.org/images/cloud/trixie/latest/debian-13-generic-amd64.qcow2`
Make it into a template with id `500`

reference: `https://pycvala.de/blog/proxmox/create-your-own-debian-12-cloud-init-template/`

```bash
# download cloud init image
wget https://cloud.debian.org/images/cloud/trixie/latest/debian-13-generic-amd64.qcow2

# create vm template
TEMPLATE_ID=500
VM_ID=501
qm create $TEMPLATE_ID --name debian13-cloudinit --memory 8192 --cores 8 \
  --net0 virtio,bridge=vmbr0 --scsihw virtio-scsi-pci --machine q35 \
  --agent enabled=1

qm importdisk $TEMPLATE_ID /root/debian-13-generic-amd64.qcow2 local-lvm
qm set $TEMPLATE_ID --scsi0 local-lvm:vm-$TEMPLATE_ID-disk-0,discard=on,ssd=1
qm disk resize $TEMPLATE_ID scsi0 64G
qm set $TEMPLATE_ID --boot order=scsi0
qm set $TEMPLATE_ID --serial0 socket --vga serial0
qm set $TEMPLATE_ID --bios ovmf --efidisk0 local-lvm:1,efitype=4m,pre-enrolled-keys=0
qm set $TEMPLATE_ID --ide2 local-lvm:cloudinit

qm template $TEMPLATE_ID

# create instance
qm clone $TEMPLATE_ID $VM_ID --name homelab-01

# configure dhcp
qm set $VM_ID --ipconfig0 ip=dhcp
qm set $VM_ID --cicustom "user=local:snippets/homelab-01-user.yaml"
```
