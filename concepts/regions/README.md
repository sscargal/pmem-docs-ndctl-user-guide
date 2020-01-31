# Regions

A generic REGION device is registered for each PMEM range or BLK-aperture set. LIBNVDIMM provides a built-in driver for these REGION devices. This driver is responsible for reconciling the aliased DPA mappings across all regions, parsing the LABEL, if present, and then emitting NAMESPACE devices with the resolved/exclusive DPA-boundaries for the `nd_pmem` or `nd_blk` device driver to consume.

Refer to [Managing Regions](../../managing-regions.md) for more information.

