# ndctl-read-infoblock\(1\)

## NAME

ndctl-read-infoblock - read and optionally parse the info-block a namespace

## SYNOPSIS

ndctl read-infoblock  &lt;namespace0.0&gt; \[&lt;namespace1.0&gt;..&lt;namespaceN.Y&gt;\] \[&lt;options&gt;\]

## DESCRIPTION

As described in the theory of operation section of [ndctl-create-namespace](ndctl-create-namespace.md#theory-of-operation) , the raw capacity of a namespace may encapsulate a personality, or mode of operation. Specifically, the mode may be set to one of "sector", "fsdax", and "devdax". Each of those modes is defined by an info-block format that uniquely identifies the mode of operation. The read-infoblock command knows the location \(relative to the start of the namespace\) and field definition of those data structures.

Note that unlike a partition table info-block is not exposed by default, so the namespace needs to be disabled before the info-block can be accessed.

## EXAMPLE

```text
ndctl disable-namespace namespace0.0
disabled 1 namespace
ndctl read-infoblock -j namespace0.0
[
  {
    "dev":"namespace0.0",
    "signature":"NVDIMM_PFN_INFO",
    "uuid":"56b11990-66b1-4d91-9cac-ca084c051259",
    "parent_uuid":"00000000-0000-0000-0000-000000000000",
    "flags":0,
    "version":"1.3",
    "dataoff":69206016,
    "npfns":1031680,
    "mode":2,
    "start_pad":0,
    "end_trunc":0,
    "align":2097152
  }
]
```

## OPTIONS

&lt;namespace\(s\)&gt;

One or more _namespaceX.Y_ device names. The keyword _all_ can be specified to operate on every namespace in the system, optionally filtered by bus id \(see --bus= option\), or region id \(see --region= option\).

-V, --verify

Attempt to validate that the info-block is self consistent by validating the embedded checksum, and that info-block formats that contain a _parent-uuid_ attribute also match the base-uuid of the namespace.

-o, --output

Output file

-j, --json

Parse the info-block data into json.

-i, --human

Enable json output and convert number formats to human readable strings, for example show the size in terms of "KB", "MB", "GB", etc instead of a signed 64-bit numbers per the JSON interchange format \(implies --json\).

-r, --region

A _regionX_ device name, or a region id number. Restrict the operation to the specified region\(s\). The keyword _all_ can be specified to indicate the lack of any restriction, however this is the same as not supplying a --region option at all.

## Copyright

Copyright \(c\) 2016 - 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

 [ndctl-create-namespace](ndctl-create-namespace.md) , [UEFI NVDIMM Label Protocol](http://www.uefi.org/sites/default/files/resources/UEFI_Spec_2_7.pdf)

