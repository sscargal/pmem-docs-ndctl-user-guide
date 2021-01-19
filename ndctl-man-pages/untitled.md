# ndctl\(1\)

[NAME](untitled.md#name)  
[SYNOPSIS](untitled.md#synopsis)  
[OPTIONS](untitled.md#options)  
[DESCRIPTION](untitled.md#description)  
[COPYRIGHT](untitled.md#copyright)  
[SEE ALSO](untitled.md#see-also)

## NAME

ndctl − Manage "libnvdimm" subsystem devices \(Non−volatile Memory\)

## SYNOPSIS

_ndctl_ \[−−version\] \[−−help\] \[OPTIONS\] COMMAND \[ARGS\]

## OPTIONS

`−v, −−version`

Display ndctl version.

`−h, −−help`

Run ndctl help command.

## DESCRIPTION

ndctl is utility for managing the "libnvdimm" kernel subsystem. The "libnvdimm" subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the ACPI 6.0 NFIT \(NVDIMM Firmware Interface Table\). Operations supported by the tool include, provisioning capacity \(namespaces\), as well as enumerating/enabling/disabling the devices \(dimms, regions, namespaces\) associated with an NVDIMM bus.

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−create−namespace\(1\)](ndctl-create-namespace.md), [ndctl−destroy−namespace\(1\)](ndctl-destroy-namespace.md), [ndctl−check−namespace\(1\)](ndctl-check-namespace.md), [ndctl−enable−region\(1\)](ndctl-enable-region.md), [ndctl−disable−region\(1\)](ndctl-disable-region.md), [ndctl−enable−dimm\(1\)](ndctl-enable-dimm.md), [ndctl−disable−dimm\(1\)](ndctl-disable-dimm.md), [ndctl−enable−namespace\(1\)](ndctl-enable-namespace.md), [ndctl−disable−namespace\(1\)](ndctl-disable-namespace.md), [ndctl−zero−labels\(1\)](ndctl-zero-labels.md), [ndctl−read−labels\(1\)](ndctl-read-labels.md), [ndctl−inject−error\(1\)](ndctl-inject-error.md), [ndctl−list\(1\)](ndctl-list.md), _LIBNVDIMM_ [https://www.kernel.org/doc/Documentation/nvdimm/nvdimm.txt](https://www.kernel.org/doc/Documentation/nvdimm/nvdimm.txt) Overview" , _NVDIMM Driver_ [http://pmem.io/documents/NVDIMM\_Driver\_Writers\_Guide.pdf](http://pmem.io/documents/NVDIMM_Driver_Writers_Guide.pdf) Writer’s Guide"

