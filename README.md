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

    All options: --generate_image --initialize --new --copy --move --run --delete --backup --list
                --ssh --vnc --smb-follow-symlink --kill --config --establish_dirs
                --install --help

    Tldr:
    1. Create an vm from an iso:
        vm --new image_name --iso_name arch --boot_type efi --ssh_port 2222 --vnc_port 5900 --ram 4 --cpus 4 --cores 4

    2. Delete a vm image:
        vm --delete image_name

    3. Copy a vm image:
        vm --copy source_image_name destination_image_name

    4. Rename(move) a vm image:
        vm --move old_image_name new_image_name

    5. List active vms:
        vm --list

    6. List all vms:
        vm --list --all

    7. Kill vm:
        vm {{ image_name }}
        vm --pid {{ pid }}

    8. Start ssh or vnc to an active vm:
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

    -g|--generate_image: create new vm image named {{ image_name }}
        vm -g image_name image_size

        defaults:
            image_size  : 4GB

    -i|--initialize: initialize vm image named {{ image_name }} with {{ iso_name }}
        vm -i image_name --iso_name arch --boot_type

        necessary: image_name, --iso_name
        defaults:
            --boot_type     : efi
            --ssh_port      : 2222
            --vnc_port      : 5900
            --image_size    : 4GB
            --ram           : 4GB
            --cpus          : 4
            --cores         : 4
            --ssh_user_name : no default

    -n|--new|--setup: create and initialize vm image named {{ image_name }} with {{ iso_name }}
        vm -n image_name --iso_name arch --image_size 4 --boot_type efi

        necessary: image_name, --iso_name
        defaults:
            same as initialize option (see above)

    -x|--xerox|--copy: copy vm image
        vm -c image_name

    -m|--move: mv vm image (rename)
        vm -m image_name

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

    -c|--config: add config for vm image
        vm -a image_name --boot_type efi --ssh_port 2222 --vnc_port 5900

        necessary: image_name
        defaults:
            --boot_type     : efi
            --ssh_port      : 2222
            --vnc_port      : 5900
            --ram           : 4GB
            --cpus          : 4
            --cores         : 4
            --ssh_user_name : no default

        print config if exists:
        vm -a -p image_name

        overwrite config if already exists:
        vm -a -m image_name --boot_type legacy

        delete config if exists:
        vm -a -d image_name

        open config file:
        vm -a -o

    -e|--establish_dirs: make or remove directories required for this script
        make directories:
        vm -e

        remove directories:
        vm -e -r

    -z|--install: install or uninstall script
        install:
        vm -z

        uninstall:
        vm -z -u

    -u|--bash_completion: setup bash completion for this script
        vm -u

    -h|--help: print this help page
