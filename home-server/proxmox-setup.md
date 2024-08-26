- install proxmox ve iso
- use rufus to convert harddrive to a bootable USB
- insert bootable USB into home server (in this case, old desktop)
- spam F2 (or ??) to go into BIOS , change boot sequence to bootable USB first
- ensure virtualization is enabled for VMs

Install proxmox with ethernet connection
Find MAC address of desktop
Set up static IP address configuration by going to Router settings (should be 'Default Gateway . . . . . . . . . : 192.168.1.254')

## VM

- Create VM (able to connect through ssh using local ip address)

```bash
ssh aloysiustanrs@192.168.1.67
```

- Update VM

```bash
sudo apt upgrade && sudo apt dist-upgrade
```

## VM templates (still unsure...)

- Create a VM
- Remove SSH host keys
- Clean machine-id file

```bash
sudo apt clean
sudo apt autoremove
```

- convert to template
- create VM using new template

## Containers

- proxmox uses LXC (Linux Containers)
