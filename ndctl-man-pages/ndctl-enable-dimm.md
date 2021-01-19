# ndctl−enable−dimm\(1\)

[NAME](ndctl-enable-dimm.md#name)  
[SYNOPSIS](ndctl-enable-dimm.md#synopsis)  
[DESCRIPTION](ndctl-enable-dimm.md#description)  
[OPTIONS](ndctl-enable-dimm.md#options)  
[COPYRIGHT](ndctl-enable-dimm.md#copyright)  
[SEE ALSO](ndctl-enable-dimm.md#see-also)

## NAME

ndctl−enable−dimm − enable one more dimms

## SYNOPSIS

_ndctl enable−dimm_  &lt;dimm&gt; \[&lt;options&gt;\]

## DESCRIPTION

A generic DIMM device object, named /dev/nmemX, is registered for each memory device indicated in the ACPI NFIT table, or other platform NVDIMM resource discovery mechanism. The LIBNVDIMM core provides a built−in driver for these DIMM devices. The driver is responsible for determining if the DIMM implements a namespace label area, and initializing the kernel’s in−memory copy of that label data.

The kernel performs runtime modifications of that data when namespace provisioning actions are taken, and actively blocks userspace from initiating label data changes while the DIMM is active in any region. Disabling a DIMM, after all the regions it is a member of have been disabled, allows userspace to manually update the label data to be consumed when the DIMM is next enabled.

## OPTIONS

A _nmemX_ device name, or a dimm id number. The keyword _all_ can be specified to carry out the operation on every dimm in the system, optionally filtered by bus id \(see −−bus= option\).

`−b, −−bus=`

Enforce that the operation only be carried on devices that are attached to the given bus. Where _bus_ can be a provider name or a bus id number.

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−disable−dimm\(1\)](ndctl-disable-dimm.md)

