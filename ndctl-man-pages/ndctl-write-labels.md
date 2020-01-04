# ndctl−write−labels\(1\)

[NAME](ndctl-write-labels.md#name)  
[SYNOPSIS](ndctl-write-labels.md#synopsis)  
[DESCRIPTION](ndctl-write-labels.md#description)  
[OPTIONS](ndctl-write-labels.md#options)  
[SEE ALSO](ndctl-write-labels.md#see-also)

## NAME

ndctl−write−labels − write data to the label area on a dimm

## SYNOPSIS

_ndctl write−labels  &lt;nmem&gt; \[-i &lt;filename&gt;\]_

## DESCRIPTION

The namespace label area is a small persistent partition of capacity available on some NVDIMM devices. The label area is used to resolve aliasing between _pmem_ and _blk_ capacity by delineating namespace boundaries. Read data from the input filename, or stdin, and write it to the given  device. Note that the device must not be active in any region, otherwise the kernel will not allow write access to the device’s label data area.

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

−i, −−input

input file

## SEE ALSO

_UEFI NVDIMM Label Protocol_ [http://www.uefi.org/sites/default/files/resources/UEFI\_Spec\_2\_7.pdf](http://www.uefi.org/sites/default/files/resources/UEFI_Spec_2_7.pdf)

