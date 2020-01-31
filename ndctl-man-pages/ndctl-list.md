# ndctl−list\(1\)

[NAME](ndctl-list.md#name)  
[SYNOPSIS](ndctl-list.md#synopsis)  
[EXAMPLE](ndctl-list.md#example)  
[OPTIONS](ndctl-list.md#options)  
[COPYRIGHT](ndctl-list.md#copyright)  
[SEE ALSO](ndctl-list.md#see-also)

## NAME

ndctl−list − dump the platform nvdimm device topology and attributes in json

## SYNOPSIS

_ndctl list_ \[&lt;options&gt;\]

Walk all the nvdimm buses in the system and list all attached devices along with some of their major attributes.

Options can be specified to limit the output to devices of a certain class. Where the classes are buses, dimms, regions, and namespaces. By default, _ndctl list_ with no options is equivalent to:

```text
ndctl list −−namespaces −−bus=all −−region=all
```

## EXAMPLE

```text
# ndctl list --buses --namespaces

{
 "provider":"nfit_test.1",
 "dev":"ndbus2",
 "namespaces":[
   {
	 "dev":"namespace9.0",
	 "mode":"raw",
	 "size":33554432,
	 "blockdev":"pmem9"
   }
 ]
}
{
 "provider":"nfit_test.0",
 "dev":"ndbus1"
}
{
 "provider":"e820",
 "dev":"ndbus0",
 "namespaces":[
   {
	 "dev":"namespace0.0",
	 "mode":"fsdax",
	 "size":8589934592,
	 "blockdev":"pmem0"
   }
 ]
}
```

## OPTIONS

−r, −−region=

A _regionX_ device name, or a region id number. The keyword _all_ can be specified to carry out the operation on every region in the system, optionally filtered by bus id \(see −−bus= option\).

−b, −−bus=

Enforce that the operation only be carried on devices that are attached to the given bus. Where _bus_ can be a provider name or a bus id number.

−d, −−dimm=

An _nmemX_ device name, or dimm id number. The dimm id number here is X in _nmemX_. Filter listing by devices that reference the given dimm. For example to see all namespaces comprised of storage capacity on nmem0:

```text
# ndctl list −−dimm=nmem0 −−namespaces
```

−n, −−namespace=

An _namespaceX.Y_ device name, or namespace region plus id tuple _X.Y_. Limit the namespace list to the single identified device if present.

−t, −−type=

Filter listing by region type \(_pmem_ or _blk_\)

−m, −−mode=

Filter listing by the mode \(_raw_, _fsdax_, _sector_ or _devdax_\) of the namespace\(s\).

−U, −−numa−node=

Filter listing by numa node

−B, −−buses

Include bus info in the listing

−D, −−dimms

Include dimm info in the listing

```text
{
 "dev":"nmem0",
 "id":"cdab-0a-07e0-ffffffff",
 "handle":0,
 "phys_id":0,
 "security:":"disabled"
}
```

−H, −−health

Include dimm health info in the listing. For example:

```text
{
 "dev":"nmem0",
 "health":{
   "health_state":"non-critical",
   "temperature_celsius":23,
   "spares_percentage":75,
   "alarm_temperature":true,
   "alarm_spares":true,
   "temperature_threshold":40,
   "spares_threshold":5,
   "life_used_percentage":5,
   "shutdown_state":"clean"
 }
}
```

−F, −−firmware

Include dimm firmware info in the listing. For example:

```text
{
 "dev":"nmem0",
 "firmware":{
	 "current_version":0,
	 "next_version":1,
	 "need_powercycle":true
 }
}
```

−X, −−device−dax

Include device−dax \("daxregion"\) details when a namespace is in "devdax" mode.

```text
{
 "dev":"namespace0.0",
 "mode":"devdax",
 "size":4225761280,
 "uuid":"18ae1bbb-bb62-4efc-86df-4a5caacb5dcc",
 "daxregion":{
   "id":0,
   "size":4225761280,
   "align":2097152,
   "devices":[
	 {
	   "chardev":"dax0.0",
	   "size":4225761280
	 }
   ]
 }
}
```

−R, −−regions

Include region info in the listing

−N, −−namespaces

Include namespace info in the listing. Namespace info is listed by default if no other options are specified to the command.

−i, −−idle

Include idle \(not enabled\) devices in the listing

−C, −−capabilities

Include region capabilities in the listing, i.e. supported namespace modes and variable properties like sector sizes and alignments.

−M, −−media−errors

Include media errors \(badblocks\) in the listing. Note that the _badblock\_count_ property is included in the listing by default when the count is non−zero, otherwise it is hidden. Also, if the namespace is in _sector_ mode the _badblocks_ listing is not included and _badblock\_count_ property may include blocks that are located in metadata, or unused capacity in the namespace. Convert a _sector_ namespace into _raw_ mode to list precise _badblocks_ offsets.

```text
{
 "dev":"namespace7.0",
 "mode":"raw",
 "size":33554432,
 "blockdev":"pmem7",
 "badblock_count":17,
 "badblocks":[
   {
	 "offset":4,
	 "length":1
   },
   {
	 "offset":32768,
	 "length":8
   },
   {
	 "offset":65528,
	 "length":8
   }
 ]
}
```

−v, −−verbose

Increase verbosity of the output. This can be specified multiple times to be even more verbose on the informational and miscellaneous output, and can be used to override omitted flags for showing specific information.

• **−v** In addition to the enabled namespaces default output, show the numa\_node, raw\_uuid, and bad block media errors.

• **−vv** Everything _−v_ provides, plus automatically enable −−dimms, −−buses, and −−regions.

• **−vvv** Everything _−vv_ provides, plus −−health, −−capabilities, −−idle, and −−firmware.

−u, −−human

Format numbers representing storage sizes, or offsets as human readable strings with units instead of the default machine−friendly raw−integer data. Convert other numeric fields into hexadecimal strings.

```text
# ndctl list --region=7
{
 "dev":"region7",
 "size":67108864,
 "available_size":67108864,
 "type":"pmem",
 "iset_id":-6382611090938810793,
 "badblock_count":8
}

# ndctl list --human --region=7
{
 "dev":"region7",
 "size":"64.00 MiB (67.11 MB)",
 "available_size":"64.00 MiB (67.11 MB)",
 "type":"pmem",
 "iset_id":"0xa76c6907811fae57",
 "badblock_count":8
}
```

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[ndctl−create−namespace\(1\)](ndctl-create-namespace.md)

