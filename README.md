# LightVM
LightVM is a virtualization solution based on Xen that is optimized to offer fast boot-times regardless of the number of active VMs. This is achieved by replacing Xenstore with a new distributed solution called ``noxs`` (no Xenstore) which provides a shared page for each device containing all the information needed for device initialization.

LightVM uses the new ``chaos`` toolstack which currently implements operations such as instantiation, saving, restoring and migration. ``chaos`` can also be used in Xen environments based on Xenstore, making it a streamlined alternative for the ``xl`` toolstack. VMs management is assisted by the XenDevD daemon for proper device initialization.

Currently, LightVM relies on Linux kernel for dom0, while for unprivileged domains one can use both Linux and Mini-OS based guests.

## Xen
* Repo: [https://github.com/cnplab/xen](https://github.com/cnplab/xen)
* Branch: ``noxs-4.8.1`` based on Xen 4.8.1
* Branch: ``noxs-4.8.0`` based on Xen 4.8.0

## Linux
* Repo: [https://github.com/cnplab/linux](https://github.com/cnplab/linux)
* Branch: ``noxs``

## XenDevD
* Repo: [https://github.com/cnplab/xendevd](https://github.com/cnplab/xendevd)
* Branch: ``noxs``

## Chaos
* Repo: [https://github.com/cnplab/chaos](https://github.com/cnplab/chaos)
* Branch: ``master``

## Mini-OS
* Repo: [https://github.com/cnplab/mini-os](https://github.com/cnplab/mini-os)
