# ndctl−check−namespace\(1\)

[NAME](ndctl-check-labels.md#name)  
[SYNOPSIS](ndctl-check-namespace.md#synopsis)  
[DESCRIPTION](ndctl-check-namespace.md#description)  
[EXAMPLES](ndctl-check-namespace.md#examples)  
[OPTIONS](ndctl-check-namespace.md#options)  
[COPYRIGHT](ndctl-check-namespace.md#copyright)  
[SEE ALSO](ndctl-check-namespace.md#see-also)

## NAME

ndctl−check−namespace − check namespace metadata consistency

## SYNOPSIS

_ndctl check−namespace_  &lt;namespace&gt; \[&lt;options&gt;\]

## DESCRIPTION

A namespace in the _sector_ mode will have metadata on it to describe the kernel BTT \(Block Translation Table\). The check−namespace command can be used to check the consistency of this metadata, and optionally, also attempt to repair it, if it has enough information to do so.

The namespace being checked has to be disabled before initiating a check on it as a precautionary measure. The `−−force` option can override this.

## EXAMPLES

Check a namespace \(only report errors\)

```text
ndctl disable−namespace namespace0.0
ndctl check−namespace namespace0.0
```

Check a namespace, and perform repairs if possible

```text
ndctl disable−namespace namespace0.0
ndctl check−namespace −−repair namespace0.0
```

## OPTIONS

−R, −−repair

Perform metadata repairs if possible. Without this option, the raw namespace contents will not be touched.

−L, −−rewrite−log

Regenerate the BTT log and write it to media. This can be used to convert from the old \(pre 4.15\) padding format that was incompatible with other BTT implementations to the updated format. This requires the `−−repair` option to be provided.

WARNING: Do not interrupt this operation as it can potentially cause unrecoverable metadata corruption. It is highly recommended to create a backup of the raw namespace before attempting this.

−f, −−force

Unless this option is specified, a check−namespace operation will fail if the namespace is presently active. Specifying `−−force` causes the namespace to be disabled before checking.

−v, −−verbose

Emit debug messages for the namespace check process.

−r, −−region=

A _regionX_ device name, or a region id number. The keyword _all_ can be specified to carry out the operation on every region in the system, optionally filtered by bus id \(see `−−bus=` option\).

−b, −−bus=

Enforce that the operation only be carried on devices that are attached to the given bus. Where _bus_ can be a provider name or a bus id number.

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−disable−namespace\(1\)](ndctl-disable-namespace.md), [ndctl−enable−namespace\(1\)](ndctl-enable-namespace.md), _UEFI NVDIMM Label Protocol_ [http://www.uefi.org/sites/default/files/resources/UEFI\_Spec\_2\_7.pdf](http://www.uefi.org/sites/default/files/resources/UEFI_Spec_2_7.pdf)

