# Quick Start

The `ndctl` command is designed to be user friendly. Once [installed](installing-ndctl/), a list of commands can be shown using any of the following:

1\) With no arguments or options, `ndctl` and `daxctl` show a simple usage message:

```text
# ndctl

 usage: ndctl [--version] [--help] COMMAND [ARGS]


 See 'ndctl help COMMAND' for more information on a specific command.
 ndctl --list-cmds to see all available commands
```

```text
# daxctl

 usage: daxctl [--version] [--help] COMMAND [ARGS]


 See 'daxctl help COMMAND' for more information on a specific command.
 daxctl --list-cmds to see all available commands

```

2\) Using `ndctl help` and `daxctl help` displays basic help and syntax:

```text
# ndctl help

 usage: ndctl [--version] [--help] COMMAND [ARGS]

 See 'ndctl help COMMAND' for more information on a specific command.
 ndctl --list-cmds to see all available commands

```

```text
# daxctl help

 usage: daxctl [--version] [--help] COMMAND [ARGS]


 See 'daxctl help COMMAND' for more information on a specific command.
 daxctl --list-cmds to see all available commands

```

Below is an example of using the `ndctl help` command to launch the `create-namespace` man page:

```text
# ndctl help create-namespace
```

3\) Using `ndctl --list-cmds` and `daxctl --list-cmds`lists all commands as a single list.

```text
# ndctl --list-cmds
version
enable-namespace
disable-namespace
create-namespace
destroy-namespace
read-infoblock
write-infoblock
check-namespace
clear-errors
enable-region
disable-region
enable-dimm
disable-dimm
zero-labels
read-labels
write-labels
init-labels
check-labels
inject-error
update-firmware
inject-smart
wait-scrub
start-scrub
setup-passphrase
update-passphrase
remove-passphrase
freeze-security
sanitize-dimm
load-keys
wait-overwrite
list
monitor
help
```

```text
# daxctl --list-cmds
version
list
help
migrate-device-model
reconfigure-device
online-memory
offline-memory
```

An alternative method for listing commands uses the TAB key completion feature of `ndctl` and `daxctl`. By typing`ndctl <TAB> <TAB>` or `daxctl <TAB> <TAB>` we can list the available commands, eg:

```text
# ndctl <TAB> <TAB>
check-labels        freeze-security     sanitize-dimm
check-namespace     help                setup-passphrase
clear-errors        init-labels         start-scrub
create-namespace    inject-error        update-firmware
destroy-namespace   inject-smart        update-passphrase
disable-dimm        list                version
disable-namespace   load-keys           wait-overwrite
disable-region      monitor             wait-scrub
enable-dimm         read-infoblock      write-infoblock
enable-namespace    read-labels         write-labels
enable-region       remove-passphrase   zero-labels
```

```text
# daxctl <TAB> <TAB>
version 	list	help	migrate-device-model	
reconfigure-device	online-memory	offline-memory
```

## TAB Command and Argument Completion

`ndctl` and `daxctl`supports command completion using the TAB key. For example, typing `ndctl enable-<TAB>` lists all commands beginning with 'enable', eg:

```text
# ndctl enable-<TAB>
enable-dimm        enable-namespace   enable-region
```

TAB completion also works with command arguments. For example, typing `ndctl enable-dimm <TAB>` will show all available command arguments. For example, the 'enable-dimm' command can enable one, more than one, or all NVDIMMs. It will list all available NVDIMMs \(nmem\) devices when using the TAB completion, eg:

```text
# ndctl enable-dimm <TAB>
all     nmem0
```

## Getting Help

NDCTL ships with a man page for each command. Each man page describes the required arguments and features in detail. Man pages can be found and accessed using the `man` or `ndctl` utilities. The following `man -k ndctl` searches for any man page containing the "ndctl" keyword:

```text
# man -k ndctl
ndctl (1)            - Manage "libnvdimm" subsystem devices (Non-volatile Memory)
ndctl-check-labels (1) - determine if the given dimms have a valid namespace index block
ndctl-check-namespace (1) - check namespace metadata consistency
ndctl-clear-errors (1) - clear all errors (badblocks) on the given namespace
ndctl-create-namespace (1) - provision or reconfigure a namespace
ndctl-destroy-namespace (1) - destroy the given namespace(s)
ndctl-disable-dimm (1) - disable one or more idle dimms
ndctl-disable-namespace (1) - disable the given namespace(s)
ndctl-disable-region (1) - disable the given region(s) and all descendant namespaces
ndctl-enable-dimm (1) - enable one more dimms
ndctl-enable-namespace (1) - enable the given namespace(s)
ndctl-enable-region (1) - enable the given region(s) and all descendant namespaces
ndctl-freeze-security (1) - Set the given DIMM(s) to reject future security operations
ndctl-init-labels (1) - initialize the label data area on a dimm or set of dimms
ndctl-inject-error (1) - inject media errors at a namespace offset
ndctl-inject-smart (1) - perform smart threshold/injection operations on a DIMM
ndctl-list (1)       - dump the platform nvdimm device topology and attributes in json
ndctl-load-keys (1)  - load the kek and encrypted passphrases into the keyring
ndctl-monitor (1)    - Monitor the smart events of nvdimm objects
ndctl-read-infoblock (1) - read and optionally parse the info-block a namespace
ndctl-read-labels (1) - read out the label area on a dimm or set of dimms
ndctl-remove-passphrase (1) - Stop a DIMM from locking at power-loss and requiring a passphrase to access media
ndctl-sanitize-dimm (1) - Perform a cryptographic destruction or overwrite of the contents of the given NVDIMM(s)
ndctl-setup-passphrase (1) - setup and enable the security passphrase for an NVDIMM
ndctl-start-scrub (1) - start an Address Range Scrub (ARS) operation
ndctl-update-firmware (1) - provides for updating the firmware on an NVDIMM
ndctl-update-passphrase (1) - update the security passphrase for an NVDIMM
ndctl-wait-overwrite (1) - wait for an overwrite operation to complete
ndctl-wait-scrub (1) - wait for an Address Range Scrub (ARS) operation to complete
ndctl-write-infoblock (1) - generate and write an infoblock
ndctl-write-labels (1) - write data to the label area on a dimm
ndctl-zero-labels (1) - zero out the label area on a dimm or set of dimms
```

```text
#  man -k daxctl
daxctl (1)           - Provides enumeration and provisioning commands for the Linux kernel Device-DAX facility
daxctl-list (1)      - dump the platform Device-DAX regions, devices, and attributes in json.
daxctl-migrate-device-model (1) - Opt-in to the /sys/bus/dax device-model, allow for alternative Device-DAX instance drivers.
daxctl-offline-memory (1) - Offline the memory for a device that is in system-ram mode
daxctl-online-memory (1) - Online the memory for a device that is in system-ram mode
daxctl-reconfigure-device (1) - Reconfigure a dax device into a different mode
```

{% hint style="info" %}
Note: If `man -k ndctl` returns "ndctl: nothing appropriate." or similar, see the [Troubleshooting](troubleshooting.md) section to manually build the indexes.
{% endhint %}

Additionally, executing `ndctl help <command>` can be used to display the man page for the command, eg:

```text
# ndctl help enable-dimm
```

A list of ndctl and daxctl man pages are available online. See [NDCTL Man Pages](ndctl-man-pages/) and [DAXCTL Man Pages](daxctl-man-pages/) for a complete list.

## Displaying Bus, NVDIMM, Region, and Namespace Information

The `ndctl list` command is a very powerful and feature rich command. A list of options is shown below:

```text
# ndctl list -?
  Error: unknown switch `?'

 usage: ndctl list [<options>]

    -b, --bus <bus-id>    filter by bus
    -r, --region <region-id>
                          filter by region
    -d, --dimm <dimm-id>  filter by dimm
    -n, --namespace <namespace-id>
                          filter by namespace id
    -m, --mode <namespace-mode>
                          filter by namespace mode
    -t, --type <region-type>
                          filter by region-type
    -U, --numa-node <numa node>
                          filter by numa node
    -B, --buses           include bus info
    -D, --dimms           include dimm info
    -F, --firmware        include firmware info
    -H, --health          include dimm health
    -R, --regions         include region info
    -N, --namespaces      include namespace info (default)
    -X, --device-dax      include device-dax info
    -C, --capabilities    include region capability info
    -i, --idle            include idle devices
    -M, --media-errors    include media errors
    -u, --human           use human friendly number formats
    -v, --verbose         increase output detail
```

Using the filters is a powerful way to limit the output.

### Examples

To list all active/enabled namespaces:

```text
# ndctl list -N
```

To list all active/enabled regions:

```text
# ndctl list -R
```

To list all active/enabled NVDIMMs:

```text
# ndctl list -D
```

To list all active/enabled NVDIMMs, Regions, and Namespaces:

```text
# ndctl list -DRN
```

To list all active/enabled and disabled/inactive \(idle\) NVDIMMs, Regions, and Namespaces:

```text
# ndctl list -DRNi
```

To list all active/enabled and disabled/inactive \(idle\) NVDIMMs, Regions, and Namespaces with human readable values:

```text
# ndctl list -iNuRD
```

## Increasing output verbosity

The `-v, --verbose` option increases the output verbosity of the command. Using `-vv` or -`-vvv` further increases the output and verbosity.

