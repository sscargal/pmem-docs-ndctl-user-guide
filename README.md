# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v66

This release incorporates functionality up to the 5.3 kernel, and adds a number of bug fixes, and improvements.

Highlights include a new command to reconfigure dax devices to different modes \(devdax - default, and system-ram - to hotplug the dax device as system memory\), improvements to ndctl-{read,write,init}-labels allowing smaller sized reads/writes, usability fixes to ndctl-monitor, and ndctl-create-namespace, and a fix to ndctl-check-namespace allowing it to be used on systems with different page sizes.

Commands: 

* [daxctl-reconfigure-device](daxctl-man-pages/daxctl-reconfigure-device.md): new command for device mode management 
* [daxctl-online-memory](daxctl-man-pages/untitled-3.md), [daxctl-offline-memory](daxctl-man-pages/daxctl-offline-memory.md): new commands for devices in system-ram mode 
* [monitor](ndctl-man-pages/ndctl-monitor.md): logging improvements, allow sending to background 
* [inject-error](ndctl-man-pages/ndctl-inject-error.md): refuse to operate on active BTT namespaces 
* [read-labels](ndctl-man-pages/ndctl-read-labels.md), [write-labels](ndctl-man-pages/ndctl-write-labels.md), [zero-labels](ndctl-man-pages/ndctl-zero-labels.md): improvements to minimize data transfer 
* [create-namespace](ndctl-man-pages/ndctl-create-namespace.md): usability improvements around region search

APIs: 

* ndctl\_cmd\_cfg\_read\_set\_extent 
* ndctl\_cmd\_cfg\_write\_set\_extent 
* ndctl\_dimm\_read\_label\_extent 
* ndctl\_dimm\_read\_label\_index 
* ndctl\_dimm\_zero\_label\_extent 
* daxctl\_dev\_disable 
* daxctl\_dev\_enable\_devdax 
* daxctl\_dev\_enable\_ram 
* daxctl\_dev\_get\_ctx 
* daxctl\_dev\_get\_memory
* daxctl\_dev\_get\_resource 
* daxctl\_dev\_get\_target\_node 
* daxctl\_dev\_is\_enabled 
* daxctl\_memory\_get\_block\_size 
* daxctl\_memory\_get\_dev 
* daxctl\_memory\_get\_node\_path 
* daxctl\_memory\_is\_online 
* daxctl\_memory\_num\_sections 
* daxctl\_memory\_offline 
* daxctl\_memory\_online

