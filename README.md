# vm

**vm** is a bash script for managing multiple virtual machines on a system

### Install

```bash
./vm --install
```

### Uninstall

```bash
./vm --install -u
```

### TLDR

    All options: --create_image --initialize --new --run --delete --backup --list
                --ssh --vnc --smb-follow-symlink --kill --add_config --make_dirs
                --install --help

    Tldr:
    1. Create an vm from an iso:
        vm --new image_name --iso_name arch --boot_type efi --ssh_port 2222 --vnc_port 5900

    2. Delete a vm image:
        vm --delete image_name

    3. List active vms:
        vm --list

    4. List all vms:
        vm --list --all

    5. Kill vm:
        vm {{ image_name }}
        vm --pid {{ pid }}

    6. Start ssh or vnc to an active vm:
        vm --ssh {{ image_name }}
        vm --vnc {{ image_name }}

### Example Config:

    [arch-linux-systemd]
    boot_type=legacy
    ssh_port=2222
    vnc_port=5900

    [debian]
    boot_type=legacy
    ssh_port=2223
    vnc_port=5901

### Defaults for dirs:

These can be changed inside script (for now):

- **ovmf file**: /usr/share/edk2-ovmf/x64
- **isos of os(es)**: $HOME/Downloads/isos

- **config directory for vms**: $HOME/.config/vm
- **config file for vms**: $HOME/.config/vm/config.vm
- **images of vms**: $HOME/.config/vm/images
- **ovmf vars for each vm**: $HOME/.config/vm/ovmf
- **backup folder**: $HOME/.config/vm/backup

- **samba share directory**: $HOME/shared

### All Options:

    -c|--create_image: create new vm image named {{ image_name }}
        vm -c image_name

    -i|--initialize: initialize vm image named {{ image_name }} with {{ iso_name }}
        vm -i image_name --iso_name arch --boot_type efi --ssh_port 2222 --vnc_port 5900

        necessary: image_name, --iso_name
        defaults:
            --boot-type : efi
            --ssh-port  : 2222
            --vnc-port  : 5900

    -n|--new|--setup: create and initialize vm image named {{ image_name }} with {{ iso_name }}
        vm -n image_name --iso_name arch --boot_type efi --ssh_port 2222 --vnc_port 5900

        necessary: image_name, --iso_name
        defaults:
            --boot-type : efi
            --ssh-port  : 2222
            --vnc-port  : 5900

    -r|--run: run image provided in {{ image_name }}
        vm -r image_name

    -d|--delete: backup vm image or config
        delete vm image:
        vm -d image_name

        delete vm image and backup too:
        vm -d -a image_name

    -l|--list: list active vm images or all vm images
        list active vm images:
        vm -l

        list all vm images:
        vm -l -a

    -b|--backup: backup vm image or config
        vm -b image_name
        vm -b -c

    -s|--ssh: ssh into currently running image
        vm -s image_name user_name

        defaluts:
        user_name: $USER

    -v|--vnc: attach tiger-vnc client to vm
        vm -v image_name

    -f|--smb_follow_symlinks: allow following symlinks in shared directory
        vm -f

        note: can be a security risk

    -k|--kill: kill vm with given {{ image_name }} {{ pid }} or all the vms
        vm -k image_name
        vm -k -p pid
        vm -k -a

    -a|--add_config: add config for vm image
        vm -a image_name --boot_type efi --ssh_port 2222 --vnc_port 5900

        necessary: image_name
        defaults:
            --boot-type : efi
            --ssh-port  : 2222
            --vnc-port  : 5900
        overwrite config if already exists:
        vm -a -o image_name boot_type ssh_port vnc_port

    -m|--make_dirs: make or remove directories required for this script
        make directories:
        vm -m

        remove directories:
        vm -m -r

    -z|--install: install or uninstall script
        install:
        vm -z

        uninstall:
        vm -z -u

    -u|--bash_completion: setup bash completion for this script
        vm -u

    -h|--help: print this help page
