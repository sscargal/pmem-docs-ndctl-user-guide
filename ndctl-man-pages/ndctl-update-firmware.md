# ndctl-update-firmware\(1\)

### Documentation for ndctl and daxctl

## NAME <a id="name"></a>

ndctl-update-firmware - update the firmware the given device

## SYNOPSIS <a id="synopsis"></a>

ndctl update-firmware &lt;dimm&gt; \[&lt;options&gt;\]

## DESCRIPTION <a id="description"></a>

Provide a generic interface for updating NVDIMM firmware. The use of this depends on support for the NVDIMM “family” in libndctl, the kernel needs to enable that command set, and the device itself needs to implement the command. Use “ndctl list -DF” to interrogate if firmware update is enabled. For example:

> ```text
> ndctl list -DFu -d nmem1
> {
>   "dev":"nmem1",
>   "id":"cdab-0a-07e0-ffffffff",
>   "handle":"0",
>   "phys_id":"0",
>   "security":"disabled",
>   "firmware":{
>     "current_version":"0",
>     "can_update":true
>   }
> }
> ```

## OPTIONS <a id="options"></a>

  
 A _nmemX_ device name, or a dimm id number. Restrict the operation to the specified dimm\(s\). The keyword _all_ can be specified to indicate the lack of any restriction, however this is the same as not supplying a –dimm option at all.

`-b; --bus=`  
 A bus id number, or a provider string \(e.g. “ACPI.NFIT”\). Restrict the operation to the specified bus\(es\). The keyword _all_ can be specified to indicate the lack of any restriction, however this is the same as not supplying a –bus option at all.

`-f; --firmware`  
 firmware file used to perform the update

`-i; --force`  
 Ignore in-progress Address Range Scrub and try to submit the firmware update, or ignore firmware activate arm overflows and force-arm devices.

`-A; --arm`  
 Arm a device for firmware activation. This is enabled by default when a firmware image is specified. Specify –no-arm to disable this default. Otherwise, without a firmware image, this option can be used to manually arm a device for firmware activate.

`-D; --disarm`  
 Disarm devices after uploading the firmware file, or manually disarm devices when a firmware image is not specified. –no-disarm is not accepted.

`-v; --verbose`  
 Emit debug messages for the namespace check process.

## COPYRIGHT <a id="copyright"></a>

Copyright \(c\) 2016 - 2020, Intel Corporation. License GPLv2: GNU GPL version 2 [http://gnu.org/licenses/gpl.html](http://gnu.org/licenses/gpl.html). This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

