# ndctl−init−labels\(1\)

[NAME](ndctl-init-labels.md#name)  
[SYNOPSIS](ndctl-init-labels.md#synopsis)  
[DESCRIPTION](ndctl-init-labels.md#description)  
[EXAMPLE](ndctl-init-labels.md#example)  
[OPTIONS](ndctl-init-labels.md#options)  
[COPYRIGHT](ndctl-init-labels.md#copyright)  
[SEE ALSO](ndctl-init-labels.md#see-also)

## NAME

ndctl−init−labels − initialize the label data area on a dimm or set of dimms

## SYNOPSIS

_ndctl init−labels_  &lt;nmem0&gt; \[&lt;nmem1&gt;..&lt;nmemN&gt;\] \[&lt;options&gt;\]

## DESCRIPTION

The namespace label area is a small persistent partition of capacity available on some NVDIMM devices. The label area is used to resolve aliasing between _pmem_ and _blk_ capacity by delineating namespace boundaries. By default, and in kernels prior to v4.10, the kernel only honors labels when a DIMM aliases PMEM and BLK capacity. Starting with v4.10 the kernel will honor labels for sub−dividing PMEM if all the DIMMs in an interleave set / region have a valid namespace index block.

This command can be used to initialize the namespace index block if it is missing or reinitialize it if it is damaged. Note that reinitialization effectively destroys all existing namespace labels on the DIMM.

## EXAMPLE

Find the DIMMs that comprise a given region:

```text
# ndctl list -RD --region=region1
{
 "dimms":[
   {
	 "dev":"nmem0",
	 "id":"8680-56341200"
   }
 ],
 "regions":[
   {
	 "dev":"region1",
	 "size":268435456,
	 "available_size":0,
	 "type":"pmem",
	 "mappings":[
	   {
		 "dimm":"nmem0",
		 "offset":13958643712,
		 "length":268435456
	   }
	 ]
   }
 ]
}
```

Disable that region so the DIMM label area can be written from userspace:

```text
# ndctl disable−region region1
```

Initialize labels:

```text
# ndctl init−labels nmem0
```

Re−enable the region:

```text
# ndctl enable−region region1
```

Create a namespace in that region:

```text
# ndctl create−namespace −−region=region1
```

## OPTIONS

`<dimm>`

One or more _nmemX_ device names. The keyword _all_ can be specified to operate on every dimm in the system, optionally filtered by bus id \(see −−bus= option\).

`−s, −−size=`

Limit the operation to the given number of bytes. A size of 0 indicates to operate over the entire label capacity.

`−O, −−offset=`

Begin the operation at the given offset into the label area.

`−b, −−bus=`

Limit operation to memory devices \(dimms\) that are on the given bus. Where _bus_ can be a provider name or a bus id number.

`−v, --verbose`

Turn on verbose debug messages in the library \(if ndctl was built with logging and debug enabled\).

`−f, −−force`

Force initialization of the label space even if there appears to be an existing / valid namespace index. Warning, this will destroy all defined namespaces on the dimm.

`−V, −−label−version`

Initialize with a specific version of labels from the namespace label specification. Defaults to 1.1

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−create−namespace\(1\)](ndctl-create-namespace.md), _UEFI NVDIMM Label Protocol_ [http://www.uefi.org/sites/default/files/resources/UEFI\_Spec\_2\_7.pdf](http://www.uefi.org/sites/default/files/resources/UEFI_Spec_2_7.pdf)

