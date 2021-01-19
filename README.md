# NDCTL User Guide

## Introduction

`ndctl` is a utility for managing the Linux LIBNVDIMM Kernel subsystem. It is designed to work with various non-volatile memory devices \(NVDIMMs\) from different vendors. The LIBNVDIMM subsystem defines a kernel device model and control message interface for platform NVDIMM resources like those defined by the [ACPI v6.0](http://www.uefi.org/sites/default/files/resources/ACPI_6_0_Errata_A.PDF) NFIT \(**N**VDIMM **F**irmware **I**nterface **T**able\). The latest [ACPI ](http://www.uefi.org/specifications)and [UEFI ](http://www.uefi.org/specifications)specifications can be found at [uefi.org](http://www.uefi.org). Operations supported by `ndctl` include:

* Provisioning capacity \(namespaces\)
* Enumerating Devices
* Enabling and Disabling NVDIMMs, Regions, and Namespaces
* Managing NVDIMM Labels

## What's new in v71.1

Fixes: 

* ndctl/dimm: Attempt an abort upon firmware-update-busy status 
* ndctl/dimm: Fix submit\_abort\_firmware\(\)

