# ndctl−zero−labels\(1\)

[NAME](ndctl-zero-labels.md#name)  
[SYNOPSIS](ndctl-zero-labels.md#synopsis)  
[DESCRIPTION](ndctl-zero-labels.md#description)  
[OPTIONS](ndctl-zero-labels.md#options)  
[COPYRIGHT](ndctl-zero-labels.md#copyright)  
[SEE ALSO](ndctl-zero-labels.md#see-also)

## NAME

ndctl−zero−labels − zero out the label area on a dimm or set of dimms

## SYNOPSIS

_ndctl zero−labels_  &lt;nmem0&gt; \[&lt;nmem1&gt;..&lt;nmemN&gt;\] \[&lt;options&gt;\]

## DESCRIPTION

The namespace label area is a small persistent partition of capacity available on some NVDIMM devices. The label area is used to resolve aliasing between _pmem_ and _blk_ capacity by delineating namespace boundaries. This command resets the device to its default state by deleting all labels.

## OPTIONS

One or more _nmemX_ device names. The keyword _all_ can be specified to operate on every dimm in the system, optionally filtered by bus id \(see −−bus= option\).

−s, −−size=

Limit the operation to the given number of bytes. A size of 0 indicates to operate over the entire label capacity.

−O, −−offset=

Begin the operation at the given offset into the label area.

−b, −−bus=

Limit operation to memory devices \(dimms\) that are on the given bus. Where _bus_ can be a provider name or a bus id number.

−v

Turn on verbose debug messages in the library \(if ndctl was built with logging and debug enabled\).

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

_UEFI NVDIMM Label Protocol_ [http://www.uefi.org/sites/default/files/resources/UEFI\_Spec\_2\_7.pdf](http://www.uefi.org/sites/default/files/resources/UEFI_Spec_2_7.pdf)

