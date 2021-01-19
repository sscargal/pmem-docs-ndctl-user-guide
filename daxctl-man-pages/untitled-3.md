# daxctl−online−memory\(1\)

[NAME](untitled-3.md#name)  
[SYNOPSIS](untitled-3.md#synopsis)  
[EXAMPLES](untitled-3.md#examples)  
[DESCRIPTION](untitled-3.md#description)  
[OPTIONS](untitled-3.md#options)  
[COPYRIGHT](untitled-3.md#copyright)  
[SEE ALSO](untitled-3.md#see-also)

## NAME

daxctl−online−memory − Online the memory for a device that is in system−ram mode

## SYNOPSIS

_daxctl online−memory_  &lt;dax0.0&gt; \[&lt;dax1.0&gt;...&lt;daxY.Z&gt;\] \[&lt;options&gt;\]

## EXAMPLES

• Reconfigure dax0.0 to system−ram mode, don’t online the memory

```text
# daxctl reconfigure-device --mode=system-ram --no-online --human dax0.0
{
 "chardev":"dax0.0",
 "size":"7.87 GiB (8.45 GB)",
 "target_node":2,
 "mode":"system-ram"
}
```

• Online the memory separately

```text
# daxctl online-memory dax0.0
dax0.0: 62 new sections onlined
onlined memory for 1 device
```

• Onlining memory when some sections were already online

```text
# daxctl online-memory dax0.0
dax0.0: 1 section already online
dax0.0: 61 new sections onlined
onlined memory for 1 device
```

## DESCRIPTION

Online the memory sections associated with a device that has been converted to the system−ram mode. If one or more blocks are already online, print a message about them, and attempt to online the remaining blocks.

This is complementary to the _daxctl−reconfigure−device_ command, when used with the _−−no−online_ option to skip onlining memory sections immediately after the reconfigure. In these scenarios, the memory can be onlined at a later time using _daxctl−online−memory_.

## OPTIONS

−r, −−region=

Restrict the operation to devices belonging to the specified region\(s\). A device−dax region is a contiguous range of memory that hosts one or more /dev/daxX.Y devices, where X is the region id and Y is the device instance id.

−u, −−human

By default the command will output machine−friendly raw−integer data. Instead, with this flag, numbers representing storage size will be formatted as human readable strings with units, other fields are converted to hexadecimal strings.

−v, −−verbose

Emit more debug messages

## COPYRIGHT

Copyright \(c\) 2016 − 2019, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

[daxctl−reconfigure−device\(1\)](daxctl-reconfigure-device.md), [daxctl−offline−memory\(1\)](daxctl-offline-memory.md)

