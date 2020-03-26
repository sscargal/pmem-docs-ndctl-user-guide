# Installing NDCTL & DAXCTL

The `ndctl` and `daxctl` utilities are used to manage the libnvdimm \(non-volatile memory device\) sub-system in the Linux Kernel. ndctl and daxctl are used to manage persistent memory devices and namespaces and they are required for certain [Persistent Memory Development Kit \(PMDK\)](https://pmem.io/pmdk) features. 

{% hint style="info" %}
Microsoft Windows users should visit the [Understand and Deploy Persistent Memory](https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/deploy-pmem) documentation.
{% endhint %}

The `ndctl` and `daxctl` utilities can be installed on Linux using either of the two options:

* [Install ndctl using packages](installing-ndctl-packages-on-linux.md)
* [Install ndctl using the source code](installing-ndctl-from-source-on-linux.md)

