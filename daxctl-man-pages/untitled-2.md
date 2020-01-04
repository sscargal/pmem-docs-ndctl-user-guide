# daxctl-list\(1\)

[NAME](untitled-2.md#name)  
[SYNOPSIS](untitled-2.md#synopsis)  
[EXAMPLE](untitled-2.md#example)  
[OPTIONS](untitled-2.md#options)  
[COPYRIGHT](untitled-2.md#copyright)

## NAME

daxctl−list − dump the platform Device−DAX regions, devices, and attributes in json.

## SYNOPSIS

_daxctl list_ \[&lt;options&gt;\]

Walk all the device−dax−regions in the system and list all device instances along with some of their major attributes.

Options can be specified to limit the output to objects of a certain class. Where the classes are regions or devices. By default, _daxctl list_ with no options is equivalent to:

daxctl list −−devices

## EXAMPLE

```text
# daxctl list --regions --devices

{
 "id":1,
 "devices":[
   {
	 "chardev":"dax1.0",
	 "size":3233808384
   }
 ]
}
```

## OPTIONS

−r, −−region=

A device−dax region is a contiguous range of memory that hosts one or more /dev/daxX.Y devices, where X is the region id and Y is the device instance id. The keyword _all_ can be specified to carry out the operation on every region in the system.

−d, −−dev=

Specify a dax device name, . tuple, or keyword _all_ to filter the listing. For example to list the first device instance in region1:

```text
# daxctl list --dev=1.0

{
 "chardev":"dax1.0",
 "size":3233808384
}
```

−D, −−devices

Include device−dax instance info in the listing \(default\)

−R, −−regions

Include region info in the listing

−i, −−idle

Include idle \(not enabled / zero−sized\) devices in the listing

−u, −−human

By default _daxctl list_ will output machine−friendly raw−integer data. Instead, with this flag, numbers representing storage size will be formatted as human readable strings with units, other fields are converted to hexadecimal strings. Example:

```text
# daxctl list
{
 "chardev":"dax1.0",
 "size":32828817408
}

# daxctl list --human
{
 "chardev":"dax1.0",
 "size":"30.57 GiB (32.83 GB)"
}
```

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

