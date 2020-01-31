# ndctl−wait−scrub\(1\)

[NAME](untitled-2.md#name)  
[SYNOPSIS](untitled-2.md#synopsis)  
[DESCRIPTION](untitled-2.md#description)  
[EXAMPLE](untitled-2.md#example)  
[OPTIONS](untitled-2.md#options)  
[COPYRIGHT](untitled-2.md#copyright)  
[SEE ALSO](untitled-2.md#see-also)

## NAME

ndctl−wait−scrub − wait for an Address Range Scrub \(ARS\) operation to complete

## SYNOPSIS

_ndctl wait−scrub_ \[&lt;bus-id&gt; &lt;bus-id2&gt; .. &lt;bus-idN&gt;\] \[&lt;options&gt;\]

## DESCRIPTION

NVDIMM Address Range Scrub is a capability provided by platform firmware that allows for the discovery of memory errors by system software. It enables system software to pre−emptively avoid accesses that could lead to uncorrectable memory error handling events, and it otherwise allows memory errors to be enumerated.

The kernel provides a POLL\(2\) capable sysfs file \(_scrub_\) to indicate the state of ARS. The _scrub_ file maintains a running count of ARS runs that have taken place. While a current run is in progress a _+_ character is emitted along with the current count. The _ndctl wait−scrub_ operation waits for _scrub_, across all specified buses, to indicate not in−progress at least once.

## EXAMPLE

Wait for scrub on all nvdimm buses in the system. The json listing report at the end only includes the buses that support ARS operations.

```text
# ndctl wait-scrub
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

Emit debug messages for the ARS wait process

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−start−scrub\(1\)](ndctl-start-scrub.md), _ACPI_ [http://www.uefi.org/sites/default/files/resources/ACPI%206\_2\_A\_Sept29.pdf](http://www.uefi.org/sites/default/files/resources/ACPI%206_2_A_Sept29.pdf) 6.2 Specification Section 9.20.7.2 Address Range Scrubbing \(ARS\) Overview"

