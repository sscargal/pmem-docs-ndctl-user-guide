# ndctl−destroy−namespace\(1\)

[NAME](ndctl-create-namespace.md#name)  
[SYNOPSIS](ndctl-clear-errors.md#synopsis)  
[THEORY OF OPERATION](ndctl-destroy-namespace.md#theory-of-operation)  
[OPTIONS](ndctl-destroy-namespace.md#options)  
[COPYRIGHT](ndctl-destroy-namespace.md#copyright)  
[SEE ALSO](ndctl-destroy-namespace.md#see-also)

## NAME

ndctl−destroy−namespace − destroy the given namespace\(s\)

## SYNOPSIS

_ndctl destroy−namespace_  &lt;namespace&gt; \[&lt;options&gt;\]

## THEORY OF OPERATION

The capacity of an NVDIMM REGION \(contiguous span of persistent memory\) is accessed via one or more NAMESPACE devices. REGION is the Linux term for what ACPI and UEFI call a DIMM−interleave−set, or a system−physical−address−range that is striped \(by the memory controller\) across one or more memory modules.

The UEFI specification defines the _NVDIMM Label Protocol_ as the combination of label area access methods and a data format for provisioning one or more NAMESPACE objects from a REGION. Note that label support is optional and if Linux does not detect the label capability it will automatically instantiate a "label−less" namespace per region. Examples of label−less namespaces are the ones created by the kernel’s _memmap=ss!nn_ command line option \(see the nvdimm wiki on kernel.org\), or NVDIMMs without a valid _namespace index_ in their label area.

A namespace can be provisioned to operate in one of 4 modes, _fsdax_, _devdax_, _sector_, and _raw_. Here are the expected usage models for these modes:

• fsdax: Filesystem−DAX mode is the default mode of a namespace when specifying _ndctl create−namespace_ with no options. It creates a block device \(/dev/pmemX\[.Y\]\) that supports the DAX capabilities of Linux filesystems \(xfs and ext4 to date\). DAX removes the page cache from the I/O path and allows mmap\(2\) to establish direct mappings to persistent memory media. The DAX capability enables workloads / working−sets that would exceed the capacity of the page cache to scale up to the capacity of persistent memory. Workloads that fit in page cache or perform bulk data transfers may not see benefit from DAX. When in doubt, pick this mode.

• devdax: Device−DAX mode enables similar mmap\(2\) DAX mapping capabilities as Filesystem−DAX. However, instead of a block−device that can support a DAX−enabled filesystem, this mode emits a single character device file \(/dev/daxX.Y\). Use this mode to assign persistent memory to a virtual−machine, register persistent memory for RDMA, or when gigantic mappings are needed.

• sector: Use this mode to host legacy filesystems that do not checksum metadata or applications that are not prepared for torn sectors after a crash. Expected usage for this mode is for small boot volumes. This mode is compatible with other operating systems.

• raw: Raw mode is effectively just a memory disk that does not support DAX. Typically this indicates a namespace that was created by tooling or another operating system that did not know how to create a Linux _fsdax_ or _devdax_ mode namespace. This mode is compatible with other operating systems, but again, does not support DAX operation.

## OPTIONS

A _namespaceX.Y_ device name. The keyword _all_ can be specified to carry out the operation on every namespace in the system, optionally filtered by region \(see −−region=option\)

`−r, −−region=`

A _regionX_ device name, or a region id number. The keyword _all_ can be specified to carry out the operation on every region in the system, optionally filtered by bus id \(see −−bus= option\).

`−b, −−bus=`

Enforce that the operation only be carried on devices that are attached to the given bus. Where _bus_ can be a provider name or a bus id number.

`−v, −−verbose`

Emit debug messages for the namespace operation

`−f, −−force`

Unless this option is specified the _destroy namespace_ operation will fail if the namespace is presently active. Specifying −−force causes the namespace to be disabled before the operation is attempted. However, if the namespace is mounted then the _disable namespace_ and _destroy namespace_ operations will be aborted. The namespace must be unmounted before being destroyed.

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−create−namespace\(1\)](ndctl-create-namespace.md)

