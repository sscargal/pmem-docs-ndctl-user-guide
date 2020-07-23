# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v69

This release incorporates functionality up to the 5.8 kernel.

Highlights include support for 'PAPR' NVDIMMs, a build fix for zero-length array warnings in GCC10, a new option for ndctl-monitor allowing for a timeout for epoll, and misc unit test and documentation fixes.

Commands: 

* monitor: add a new timeout option for polling list: skip region filtering if numa\_node is absent 
* {read,write}-infoblock: set a default alignment based on platform 
* list/others: support for PAPR NVDIMMs

Tests: 

* align.sh: fix region selection, and label init expectation

APIs: 

* ndctl\_bus\_has\_of\_node 
* ndctl\_bus\_is\_papr\_scm 
* ndctl\_region\_has\_numa

