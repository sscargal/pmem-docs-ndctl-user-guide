# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v68

This release incorporates functionality up to the 5.6 kernel.

Highlights for this release include new commands to read-infoblock and write-infoblock, improvements and tests related to alignment constraints, misc build/compilation related fixes, and misc usability and documentation fixes.

Commands: 

* zero-labels: display an error if regions are active 
* destroy-namespace: fix seed namespace accounting 
* list: drop named list objects from verbose listing 
* \*-namespace: emit better errors on failure 
* read-infoblock: new command to read an infoblock 
* write-infoblock: new command to create and write an infoblock

APIs: 

* ndctl\_namespace\_get\_target\_node 
* ndctl\_namespace\_is\_configuration\_idle 
* ndctl\_region\_get\_align
* ndctl\_region\_get\_target\_node 
* ndctl\_region\_set\_align

