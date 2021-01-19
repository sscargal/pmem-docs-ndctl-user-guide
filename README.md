# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v71

This release incorporates functionality up to the 5.10 kernel.

Highlights include support for the new device-dax subdivision functionality added in Linux in v5.10, including ways to create smaller devdax devices using daxctl/libdaxctl, as well as creating, listing, and restoring from a config dump, 'mappings' on these devices. Other updates include several static analysis fixups, reworking the license identification scheme for different sub-components, and a fix for the reconfigure-in-place workflow which tries to retain device names.

Commands: 

* daxctl-create-device: new command 
* daxctl-destroy-device: new command 
* daxctl-enable-device: new command 
* daxctl-disable-device: new command 
* daxctl-reconfigure-device: allow resizing devices 
* ndctl-create-namespace: improve reconfigure in-place

Tests: 

* daxctl-create.sh: new test for device-dax subdivision

APIs: 

* daxctl\_dev\_get\_align 
* daxctl\_dev\_set\_align 
* daxctl\_dev\_set\_mapping
* daxctl\_dev\_set\_size 
* daxctl\_mapping\_get\_end 
* daxctl\_mapping\_get\_first 
* daxctl\_mapping\_get\_next 
* daxctl\_mapping\_get\_offset 
* daxctl\_mapping\_get\_size 
* daxctl\_mapping\_get\_start 
* daxctl\_region\_create\_dev 
* daxctl\_region\_destroy\_dev

