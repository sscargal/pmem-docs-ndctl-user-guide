# daxctl-disable-device \(1\)

[NAME](daxctl-disable-device.md#name)  
[SYNOPSIS](daxctl-disable-device.md#synopsis)  
[EXAMPLES  
](daxctl-disable-device.md#examples)[DESCRIPTION](daxctl-disable-device.md#description)[  
](daxctl-create-device.md#examples)[OPTIONS](daxctl-disable-device.md#options)  
[COPYRIGHT](daxctl-disable-device.md#copyright)  
[SEE ALSO](daxctl-disable-device.md#see-also)

## NAME <a id="name"></a>

daxctl-disable-device - Disables a devdax device

## SYNOPSIS <a id="synopsis"></a>

daxctl disable-device \[&lt;options&gt;\]

## EXAMPLES <a id="examples"></a>

* Disables dax0.1

```text
# daxctl disable-device dax0.1
```

* Disables all devices in region id 0

```text
# daxctl disable-device -r 0 all
disabled 3 devices
```

## DESCRIPTION <a id="description"></a>

Disables a dax device in _devdax_ mode.

## OPTIONS <a id="options"></a>

`-r; --region=`  
 Restrict the operation to devices belonging to the specified region\(s\). A device-dax region is a contiguous range of memory that hosts one or more /dev/daxX.Y devices, where X is the region id and Y is the device instance id.

`-u; --human`  
 By default the command will output machine-friendly raw-integer data. Instead, with this flag, numbers representing storage size will be formatted as human readable strings with units, other fields are converted to hexadecimal strings.

`-v; --verbose`  
 Emit more debug messages

## COPYRIGHT <a id="copyright"></a>

Copyright © 2016 - 2020, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO <a id="see-also"></a>

[daxctl-list](untitled-2.md),[daxctl-reconfigure-device](daxctl-reconfigure-device.md),[daxctl-create-device](daxctl-create-device.md)

