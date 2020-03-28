# daxctl−offline−memory\(1\)

[NAME](daxctl-offline-memory.md#name)  
[SYNOPSIS](daxctl-offline-memory.md#synopsis)  
[EXAMPLES](daxctl-offline-memory.md#examples)  
[DESCRIPTION](daxctl-offline-memory.md#description)  
[OPTIONS](daxctl-offline-memory.md#options)  
[COPYRIGHT](daxctl-offline-memory.md#copyright)  
[SEE ALSO](daxctl-offline-memory.md#see-also)

## NAME

daxctl−offline−memory − Offline the memory for a device that is in system−ram mode

## SYNOPSIS

_daxctl offline−memory_  &lt;dax0.0&gt; \[&lt;dax1.0&gt;...&lt;daxY.Z&gt;\] \[&lt;options&gt;\]

## EXAMPLES

• Reconfigure dax0.0 to system−ram mode

```text
# daxctl reconfigure-device --mode=system-ram --human dax0.0
{
 "chardev":"dax0.0",
 "size":"7.87 GiB (8.45 GB)",
 "target_node":2,
 "mode":"system-ram"
}
```

• Offline the memory

```text
# daxctl offline-memory dax0.0
dax0.0: 62 sections offlined
offlined memory for 1 device
```

## DESCRIPTION

Offline the memory sections associated with a device that has been converted to the system−ram mode. If one or more blocks are already offline, attempt to offline the remaining blocks. If all blocks were already offline, print a message and return success without actually doing anything.

This is complementary to the _daxctl−online−memory_ command, and may be used when it is wished to offline the memory sections, but not convert the device back to _devdax_ mode.

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

[daxctl−reconfigure−device\(1\)](daxctl-reconfigure-device.md), [daxctl−online−memory\(1\)](untitled-3.md)

