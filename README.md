# Base Arch playbook

Base playbook to set up an Arch box

## Running

```bash
ssh-copy-id `#ip`
ansible-playbook master.yml -e tailscale_authkey=`#key` -e ansible_host=`#ip`
```

## Installation

Used `archinstall`.  Select linux-lts kernel. Select Minimal packages & choose NetworkManager during installation. chroot in after installing and enable the sshd service.

Base packages:
```json
    "packages": [
        "intel-ucode",
        "linux-firmware",
        "neovim",
        "openssh",
        "python"
    ],
```

Firewall rules (& drift management) are handled externally by [OpenVox](https://voxpupuli.org/openvox/).

## Backups

Backups are automated using [Borg](https://www.borgbackup.org/) + the incredible [Borgbase](https://www.borgbase.com/). Local (NFS) backups are also added for some repos via my UNAS2, but because adding the export is a manual step, this part is only partially automated.

## Versions

[Renovate](https://github.com/renovatebot/renovate) is used to make PRs for containers, Ansible Galaxy collections, and AUR packages.  Other updates are handled manually by the package manager.

