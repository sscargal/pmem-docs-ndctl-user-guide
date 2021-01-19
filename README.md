# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v70

This release incorporates functionality up to the 5.9 kernel.

Highlights include support for the new firmware activation facility, a new 'split-acpi' command in 'daxctl' to aid testing and debugging, and other minor fixes.

Commands: 

* update-firmware: add support for firmware activation 
* list: updates for firmware activation 
* activate-firmware: new command to trigger firmware activation 
* daxctl-split-acpi: split ACPI tables for debugging

Tests: 

* revoke-devmem: new test to validate iomem protections 
* update-firmware: update to test firmware activation

APIs: 

* ndctl\_bus\_activate\_firmware 
* ndctl\_bus\_clear\_fw\_activate\_noidle 
* ndctl\_bus\_clear\_fw\_activate\_nosuspend 
* ndctl\_bus\_get\_fw\_activate\_method 
* ndctl\_bus\_get\_fw\_activate\_state 
* ndctl\_bus\_set\_fw\_activate\_noidle 
* ndctl\_bus\_set\_fw\_activate\_nosuspend 
* ndctl\_dimm\_fw\_activate\_arm 
* ndctl\_dimm\_fw\_activate\_disarm 
* ndctl\_dimm\_get\_fw\_activate\_result 
* ndctl\_dimm\_get\_fw\_activate\_state

