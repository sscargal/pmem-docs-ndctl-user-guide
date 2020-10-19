# ndctl−check−labels\(1\)

[NAME](ndctl-check-labels.md#name)  
[SYNOPSIS](ndctl-check-labels.md#synopsis)  
[DESCRIPTION](ndctl-check-labels.md#description)  
[OPTIONS](ndctl-check-labels.md#options)  
[COPYRIGHT](ndctl-check-labels.md#copyright)  
[SEE ALSO](ndctl-check-labels.md#see-also)

## NAME

ndctl−check−labels − determine if the given dimms have a valid namespace index block

## SYNOPSIS

_ndctl check−labels_  &lt;nmem0&gt; \[&lt;nmem1&gt;..&lt;nmemN&gt;\] \[&lt;options&gt;\]

## DESCRIPTION

The namespace label area is a small persistent partition of capacity available on some NVDIMM devices. The label area is used to resolve aliasing between _pmem_ and _blk_ capacity by delineating namespace boundaries. In addition to checking if a label area has a valid index block, running this command in verbose mode reports the reason the index block is deemed invalid.

## OPTIONS

`<memory device(s)>`

One or more _nmemX_ device names. The keyword _all_ can be specified to operate on every dimm in the system, optionally filtered by bus id \(see −−bus= option\).

`−s, −−size`

Limit the operation to the given number of bytes. A size of 0 indicates to operate over the entire label capacity.

`−O, −−offset`

Begin the operation at the given offset into the label area.

`−b, −−bus`

Limit operation to memory devices \(dimms\) that are on the given bus. Where _bus_ can be a provider name or a bus id number.

`−v`

Turn on verbose debug messages in the library \(if ndctl was built with logging and debug enabled\).

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

_UEFI NVDIMM Label Protocol_ [http://www.uefi.org/sites/default/files/resources/UEFI\_Spec\_2\_7.pdf](http://www.uefi.org/sites/default/files/resources/UEFI_Spec_2_7.pdf)

