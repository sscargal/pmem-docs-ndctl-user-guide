# Managing Regions

A region is a grouping of one or more NVDIMMs, or an interleaved set, that can be divided up into one or more Namespaces. Regions are of type PMEM or BLK. See [PMEM or BLK](concepts/libnvdimm-pmem-and-blk-modes.md) modes for more information. Regions can only be created, destroyed, and configured using the vendor specific NVDIMM utility that manages the NVDIMMs or BIOS options, if available.

## Listing Regions

Currently available regions can be shown using the `-R` or `--regions` flag to the `ndctl list` command, eg:

```text
# ndctl list --regions
[
  {
    "dev":"region1",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":-2506113243053544244,
    "persistence_domain":"memory_controller"
  },
  {
    "dev":"region0",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":3259620181632232652,
    "persistence_domain":"memory_controller"
  }
]
```

### Filtering \(Searching\) the output

The output can be filtered on any filter supported by `ndctl list`, ie `--bus`, `--region`, `--dimm`, `--namespace`, `--type`, and `--numa-node`. For example:

```text
// Show only 'region0'
# ndctl list --region region0

// Show the region used by NVDIMM 'nmem0'
# ndctl list --dimm nmem0 --regions

// Show the region used by 'namespace0.0'
# ndctl list --namespace namespace0.0 --regions
```

### Listing Disabled Regions

Disabled regions can be included in the show output using the `-Ri` or `--regions --idle` flags, eg:

```text
# ndctl list --regions --idle
[
  {
    "dev":"region1",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":-2506113243053544244,
    "persistence_domain":"memory_controller"
  },
  {
    "dev":"region0",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":3259620181632232652,
    "state":"disabled",     <----
    "persistence_domain":"memory_controller"
  }
]

```

## Disabling Regions

1\) List all active/enabled regions:

```text
# ndctl list -R
[
  {
    "dev":"region1",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":-2506113243053544244,
    "persistence_domain":"memory_controller"
  },
  {
    "dev":"region0",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":3259620181632232652,
    "persistence_domain":"memory_controller"
  }
]
```

A filtered list of active/enabled regions can be displayed using the `-r <region-id>` or `--region <region-id>` option, eg:

```text
# ndctl list -R -r region0
- or -
# ndctl list -R -region region0
```

2\) Disable the region

```text
# ndctl disable-region region0
disabled 1 region
```

3\) Verify the region is disabled by including the `-i` option:

```text
# ndctl list -Ri
[
  ...
  {
    "dev":"region0",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":3259620181632232652,
    "state":"disabled",     <---
    "persistence_domain":"memory_controller"
  }
]
```

## Enabling Regions

1\) List disabled/inactive regions

```text
# ndctl list -Ri
[
  ...
  {
    "dev":"region0",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":3259620181632232652,
    "state":"disabled",     <---
    "persistence_domain":"memory_controller"
  }
]
```

A filtered list of active/enabled regions can be displayed using the `-r <region-id>` or `--region <region-id>` option, eg:

```text
# ndctl list -R -r region0
- or -
# ndctl list -R -region region0
```

2\) Enable the region

```text
# ndctl enable-region region0
enabled 1 region
```

3\) Verify the region is enabled using `ndctl list -R`. Note the 'state' field is not displayed for enabled regions.

```text
# ndctl list -R
[
  {
    "dev":"region1",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":-2506113243053544244,
    "persistence_domain":"memory_controller"
  },
  {
    "dev":"region0",
    "size":1623497637888,
    "align":100663296,
    "available_size":1623497637888,
    "max_available_extent":1623497637888,
    "type":"pmem",
    "iset_id":3259620181632232652,
    "persistence_domain":"memory_controller"
  }
]
```

