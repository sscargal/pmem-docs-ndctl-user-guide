# daxctl-enable-device \(1\)

[NAME](daxctl-enable-device.md#name)  
[SYNOPSIS](daxctl-enable-device.md#synopsis)  
[EXAMPLES  
](daxctl-enable-device.md#examples)[DESCRIPTION](daxctl-enable-device.md#description)[  
](daxctl-create-device.md#examples)[OPTIONS](daxctl-enable-device.md#options)  
[COPYRIGHT](daxctl-enable-device.md#copyright)  
[SEE ALSO](daxctl-enable-device.md#see-also)

## NAME <a id="name"></a>

daxctl-enable-device - Enable a devdax device

## SYNOPSIS <a id="synopsis"></a>

daxctl enable-device  &lt;dax0.0&gt; \[&lt;dax1.0&gt;...&lt;daxY.Z&gt;\] \[&lt;options&gt;\]

## EXAMPLES <a id="examples"></a>

* Enables dax0.1

```text
# daxctl enable-device dax0.1
enabled 1 device
```

* Enables all devices in region id 0

```text
# daxctl enable-device -r 0 all
enabled 3 devices
```

## DESCRIPTION <a id="description"></a>

Enables a dax device in _devdax_ mode.

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

