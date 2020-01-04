# ndctl−disable−region\(1\)

[NAME](ndctl-disable-region.md#name)  
[SYNOPSIS](ndctl-disable-region.md#synopsis)  
[DESCRIPTION](ndctl-disable-region.md#description)  
[OPTIONS](ndctl-disable-region.md#options)  
[COPYRIGHT](ndctl-disable-region.md#copyright)  
[SEE ALSO](ndctl-disable-region.md#see-also)

## NAME

ndctl−disable−region − disable the given region\(s\) and all descendant namespaces

## SYNOPSIS

_ndctl disable−region_  &lt;region&gt; \[&lt;options&gt;\]

## DESCRIPTION

A generic REGION device is registered for each PMEM range or BLK−aperture set. LIBNVDIMM provides a built−in driver for these REGION devices. This driver is responsible for reconciling the aliased DPA mappings across all regions, parsing the LABEL, if present, and then emitting NAMESPACE devices with the resolved/exclusive DPA−boundaries for the nd\_pmem or nd\_blk device driver to consume.

## OPTIONS

A _regionX_ device name, or a region id number. The keyword _all_ can be specified to carry out the operation on every region in the system, optionally filtered by bus id \(see −−bus= option\).

−b, −−bus=

Enforce that the operation only be carried on devices that are attached to the given bus. Where _bus_ can be a provider name or a bus id number.

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−enable−region\(1\)](ndctl-enable-region.md)

