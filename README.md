# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v67

This release incorporates functionality up to the 5.4 kernel, and adds a number of bug fixes, and improvements.

Highlights include small changes for PowerPC compatibility, improvements to the dax.sh unit test to detect failures in mapping huge pages, support for the 'security frozen' attribute, user experience improvements for the daxctl-reconfigure-device command, including an option to specify movable vs. non-movable state for onlining memory, and an option to allow create-namespaces to create a maximal configuration until it exhausts all available region capacity.

Commands: 

* [create-namespace](ndctl-man-pages/ndctl-create-namespace.md): add --continue option 
* [daxctl-reconfigure-device](daxctl-man-pages/daxctl-reconfigure-device.md): add --no-movable option 
* [daxctl-reconfigure-device](daxctl-man-pages/daxctl-reconfigure-device.md): display movable state in listings 
* [daxctl-reconfigure-device](daxctl-man-pages/daxctl-reconfigure-device.md): detect races in memory onlining 
* security: support for 'security frozen' attribute

APIs: 

* ndctl\_dimm\_security\_is\_frozen 
* daxctl\_memory\_is\_movable 
* daxctl\_memory\_online\_no\_movable

