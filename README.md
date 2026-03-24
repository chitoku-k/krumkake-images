krumkake-images
===============

[![][workflow-badge]][workflow-link]

## Requirements

- [mkosi](https://github.com/systemd/mkosi)
- [cpio](https://www.gnu.org/software/cpio/)
- [mtools](https://www.gnu.org/software/mtools/)
- [bootctl](https://www.freedesktop.org/software/systemd/man/latest/bootctl.html)
- [python](https://www.python.org/)
  - [pefile](https://github.com/erocarrera/pefile)
- [pacman](https://gitlab.archlinux.org/pacman/pacman)
- [makepkg](https://gitlab.archlinux.org/pacman/pacman)
- [bsdtar](https://github.com/libarchive/libarchive)

### Arch Linux

```bash
pacman -Syu \
    mkosi
    cpio \
    mtools \
    python \
    python-pefile
```

### Debian

```bash
apt-get install --no-install-recommends \
    mkosi \
    cpio \
    mtools \
    systemd-boot-tools \
    python3 \
    python3-pefile \
    pacman-package-manager \
    makepkg \
    libarchive-tools
```

## Build

```bash
cd archlinux
export KUBERNETES_VERSION=v0.0.0 # https://github.com/kubernetes/kubernetes/releases
export KUBERNETES_RELEASE=v0.0.0 # https://github.com/kubernetes/release/releases
sudo \
    --preserve-env=KUBERNETES_VERSION \
    --preserve-env=KUBERNETES_RELEASE \
    mkosi --image-id="archlinux-$KUBERNETES_VERSION" --force
```

## Verify

Install [guestfs-tools](https://libguestfs.org/).

```bash
cd archlinux
export KUBERNETES_VERSION=v0.0.0 # https://github.com/kubernetes/kubernetes/releases
export KUBERNETES_RELEASE=v0.0.0 # https://github.com/kubernetes/release/releases
virt-df -a "archlinux-$KUBERNETES_VERSION"
virt-ls -a "archlinux-$KUBERNETES_VERSION" -m /dev/sda2:/ -m /dev/sda1:/boot -l /
```

[workflow-link]:    https://github.com/chitoku-k/krumkake-images/actions?query=branch:master
[workflow-badge]:   https://img.shields.io/github/actions/workflow/status/chitoku-k/krumkake-images/build.yml?branch=master&style=flat-square
