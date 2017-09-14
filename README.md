# LightVM
LightVM is a virtualization solution based on Xen that is optimized to offer fast boot-times regardless of the number of active VMs. This is achieved by replacing Xenstore with a new distributed solution called ``noxs`` (no Xenstore) which provides a shared page for each device containing all the information needed for device initialization.

LightVM uses the new ``chaos`` toolstack which currently implements operations such as instantiation, saving, restoring and migration. ``chaos`` can also be used in Xen environments based on Xenstore, making it a streamlined alternative for the ``xl`` toolstack. VMs management is assisted by the XenDevD daemon for proper device initialization.

Currently, LightVM relies on Linux kernel for dom0, while for unprivileged domains one can use both Linux and Mini-OS based guests.

## Xen
* Repo: [https://github.com/cnplab/xen](https://github.com/cnplab/xen)
* Branch: ``noxs-4.8.1`` based on Xen 4.8.1
* Branch: ``noxs-4.8.0`` based on Xen 4.8.0
* Build and installation steps are the same ones used for upstream Xen. Be sure to provide a custom installation path before building if a different location is desired.
```bash
./configure --prefix=<my Xen distribution directory>
make dist-xen
make dist-tools
```

## Linux
* Repo: [https://github.com/cnplab/linux](https://github.com/cnplab/linux)
* Branch: ``noxs``
* Build: Add ``CONFIG_XEN_NOXS=y`` in the config file in addition to using the [Xen config flags](https://wiki.xenproject.org/wiki/Mainline_Linux_Kernel_Configs#Configuring_the_Kernel) for building Linux domains.
* Prepare the userspace headers which will be used by the Chaos toolstack:
```bash
make headers_install INSTALL_HDR_PATH=<my Linux headers>
```

## XenDevD
* Repo: [https://github.com/cnplab/xendevd](https://github.com/cnplab/xendevd)
* Branch: ``noxs``
* Build: Before running ``make`` command, update the Makefile to refer to the headers and libraries installed in the previously configured Xen distribution directory:
```diff
-CFLAGS   += -Iinc -Wall -g -O3
-LDFLAGS  += -lxenstore
+CFLAGS   += -Iinc -Wall -g -O3 -I<Xen source tree>/<my Xen distribution directory>/include
+LDFLAGS  += -lxenstore -L<Xen source tree>/<my Xen distribution directory>/lib/
```

## Chaos
* Repo: [https://github.com/cnplab/chaos](https://github.com/cnplab/chaos)
* Branch: ``master``
* Build: Before building, configure the variables in the ``config.in`` file to refer to the previously configured environment paths. For build, simply run the ``make`` command. NoXS can be enabled by using the ``CONFIG_H2_XEN_NOXS`` flag:
```bash
make CONFIG_H2_XEN_NOXS=y
```

## Mini-OS
* Repo: [https://github.com/cnplab/mini-os](https://github.com/cnplab/mini-os)
