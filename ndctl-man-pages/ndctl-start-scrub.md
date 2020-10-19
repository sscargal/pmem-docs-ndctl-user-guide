# ndctl−start−scrub\(1\)

[NAME](ndctl-start-scrub.md#name)  
[SYNOPSIS](ndctl-start-scrub.md#synopsis)  
[DESCRIPTION](ndctl-start-scrub.md#description)  
[EXAMPLE](ndctl-start-scrub.md#example)  
[OPTIONS](ndctl-start-scrub.md#options)  
[COPYRIGHT](ndctl-start-scrub.md#copyright)  
[SEE ALSO](ndctl-start-scrub.md#see-also)

## NAME

ndctl−start−scrub − start an Address Range Scrub \(ARS\) operation

## SYNOPSIS

_ndctl start−scrub_ \[&lt;bus-id&gt; &lt;bus-id2&gt; .. &lt;bus-idN&gt;\] \[&lt;options&gt;\]

## DESCRIPTION

NVDIMM Address Range Scrub is a capability provided by platform firmware that allows for the discovery of memory errors by system software. It enables system software to pre−emptively avoid accesses that could lead to uncorrectable memory error handling events, and it otherwise allows memory errors to be enumerated.

The kernel provides a sysfs file \(_scrub_\) that when written with the string "1\n" initiates an ARS operation. The _ndctl start−scrub_ operation starts an ARS, across all specified buses, and the kernel in turn proceeds to scrub every persistent memory address region on the specified buses.

## EXAMPLE

Start a scrub on all nvdimm buses in the system. The json listing report only includes the buses that support ARS operations.

```text
# ndctl start-scrub
[
 {
   "provider":"nfit_test.1",
   "dev":"ndbus3",
   "scrub_state":"active"
 },
 {
   "provider":"nfit_test.0",
   "dev":"ndbus2",
   "scrub_state":"active"
 }
]
```

When specifying an individual bus, or if there is only one bus in the system, the command reports whether ARS support is available.

```text
# ndctl start−scrub e820
error starting scrub: Operation not supported
```

## OPTIONS

−v, −−verbose

Emit debug messages for the ARS start process

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−wait−scrub\(1\)](untitled-2.md), _ACPI_ [http://www.uefi.org/sites/default/files/resources/ACPI%206\_2\_A\_Sept29.pdf](http://www.uefi.org/sites/default/files/resources/ACPI%206_2_A_Sept29.pdf) 6.2 Specification Section 9.20.7.2 Address Range Scrubbing \(ARS\) Overview"

