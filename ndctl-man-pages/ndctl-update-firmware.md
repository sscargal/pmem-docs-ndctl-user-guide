# ndctl−update−firmware\(1\)

[NAME](ndctl-update-firmware.md#name)  
[SYNOPSIS](ndctl-update-firmware.md#synopsis)  
[DESCRIPTION](ndctl-update-firmware.md#description)  
[OPTIONS](ndctl-update-firmware.md#options)  
[COPYRIGHT](ndctl-update-firmware.md#copyright)

## NAME

ndctl−update−firmware − provides for updating the firmware on an NVDIMM

## SYNOPSIS

ndctl update−firmware  &lt;dimm&gt; \[&lt;options&gt;\]

## DESCRIPTION

Provide a generic interface for updating NVDIMM firmware. The use of this depends on support from the underlying libndctl, kernel, as well as the platform itself.

## OPTIONS

A _nmemX_ device name, or a dimm id number. The keyword _all_ can be specified to carry out the operation on every dimm in the system, optionally filtered by bus id \(see −−bus= option\).

−b, −−bus=

Enforce that the operation only be carried on devices that are attached to the given bus. Where _bus_ can be a provider name or a bus id number.

−f, −−firmware

firmware file used to perform the update

−v, −−verbose

Emit debug messages for the namespace check process.

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

