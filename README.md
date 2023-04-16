# vm

**vm** is a bash script for managing multiple virtual machines on a system

### Install

```bash
./vm --install
```

### Uninstall

```bash
./vm --install -r
```

### Usage:

    -c|--create_image: create new vm image named {{ image_name }}

        $(basename "$0") -c image_name

    -i|--initialize: initialize vm image named {{ image_name }} with {{ iso_name }}

        $(basename "$0") -i iso_name image_name boot_type ssh_port vnc_port

        necessary: iso_name, image_name
        defaults:
            boot-type : efi
            ssh-port  : 2222
            vnc-port  : 5900

    -n|--new|--setup: create and initialize vm image named {{ image_name }} with {{ iso_name }}

        $(basename "$0") -n iso_name image_name boot_type ssh_port vnc_port

        necessary: iso_name, image_name
        defaults:
            boot-type : efi
            ssh-port  : 2222
            vnc-port  : 5900

    -s|--start|--run: run image provided in {{ image_name }}

        $(basename "$0") -s image_name

    -r|--remove: backup vm image or config

        remove vm image:

        $(basename "$0") -r image_name

        remove vm image and backup too:

        $(basename "$0") -r -a image_name

    -p|--print|--list: list active vm images or all vm images

        list active vm images:

        $(basename "$0") -p

        list all vm images:

        $(basename "$0") -p -a

    -b|--backup: backup vm image or config

        $(basename "$0") -b image_name
        $(basename "$0") -b -c

    -l|--ssh|--login: ssh into currently running image

        $(basename "$0") -l image_name user_name

        defaluts:
        user_name: $USER

    -v|--vnc: attach tiger-vnc client to vm

        $(basename "$0") -v image_name

    -f|--smb_follow_symlinks: allow following symlinks in shared directory

        $(basename "$0") -l

        note: can be a security risk

    -k|--kill: kill vm with given {{ image_name }} {{ pid }} or all the vms

        $(basename "$0") -k image_name
        $(basename "$0") -k -p pid
        $(basename "$0") -k -a

    -z|--add_config: add config for vm image already existing

        $(basename "$0") -z image_name boot_type ssh_port vnc_port

        defaults:
            boot-type : efi
            ssh-port  : 2222
            vnc-port  : 5900

    -m|--make_dirs: make or remove directories required for this script

        make directories:

        $(basename "$0") -m

        remove directories:

        $(basename "$0") -m -r

    -j|--install: install or uninstall script

        install:

        $(basename "$0") -j

        uninstall:

        $(basename "$0") -j -r

    -u|--bash_completion: setup bash completion for this script

        $(basename "$0") -u

    -h|--help: print this help page

### Defaults for dirs:

These can currently be changed inside script

- **ovmf file**: /usr/share/edk2-ovmf/x64
- **isos of os(es)**: $HOME/Downloads/isos

- **config directory for vms**: $HOME/.config/vm
- **config file for vms**: $HOME/.config/vm/config.vm
- **images of vms**: $HOME/.config/vm/images
- **ovmf vars for each vm**: $HOME/.config/vm/ovmf
- **backup folder**: $HOME/.config/vm/backup

- **samba share directory**: $HOME/shared
