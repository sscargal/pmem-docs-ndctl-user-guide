# Managing NVDIMMs

Managing physical or emulated NVDIMMs using `ndctl` has no functional difference. Physical NVDIMM features and options may be controlled through the system BIOS. The BIOS cannot see emulated NVDIMMs.

Observe the following restrictions when managing NVDIMMs

* DO NOT change the memory slot of physical NVDIMMs when they are part of an Interleave Set.  Doing so changes the order of interleaving so data access will be compromised or corrupted.  If interleaving is disabled, moving NVDIMMs to different slot locations is okay, but not recommended.
* DO NOT disable NVDIMMs when they are part of an active Region and/or Namespace as this will prevent data access and may corrupt data.
* ALWAYS backup the data and make a copy of the configuration layout prior to any changes.

## Listing active/enabled NVDIMMs

The `ndct list -D` , or equivalent `ndct list --dimm` , can be used to show active/enabled NVDIMM devices on the system, eg:

```text
# ndctl list -D
{
  "dev":"nmem0",
  "id":"8089-a2-1809-00000107",
  "handle":1,
  "phys_id":29
}
```

## Listing disabled/inactive NVDIMMs

By default, `ndctl` only lists enabled/active dimms, regions, and namespaces. To include previously disabled \(inactive\) NVDIMMs, include the `-i` flag to show both enabled and disabled devices, eg:

```text
# ndctl list -Di
{
  "dev":"nmem0",
  "id":"8089-a2-1809-00000107",
  "handle":0,
  "phys_id":29
}
{
  "dev":"nmem1",
  "id":"9759-b5-1459-00000502",
  "handle":1,
  "phys_id":30
  "state":"disabled"
}
...
```

{% hint style="info" %}
NVDIMM vendor specific tools can be used to display more information about the NVDIMMs from the operating system layer. For example, Intel Optane DC Persistent Memory Modules can be managed using the [ipmctl](https://github.com/intel/ipmctl) utility. Refer to the [IPMCTL User Guide](https://docs.pmem.io/ipmctl-user-guide/) for more information. For other persistent memory products, refer to the vendor specific documentation.
{% endhint %}

## Disabling NVDIMMs

NVDIMMs can only be disabled if they have no active Regions or Namespaces. If an active/enabled namespace and/or region exists, a message is displayed:

```text
# ndctl disable-dimm nmem0
nmem0 is active, skipping...
disabled 0 nmem
```

1\) List the current active/enabled configuration

```text
# ndctl list -NRD
```

2\) Verify no fsdax or devdax namespaces are mounted or in-use by running applications

3\) Destroy or disable any active/enabled namespace\(s\).

```text
# ndctl disable-namespace <namespaceX.Y>
- or -
# ndctl destroy-namespace <namespaceX.Y>
```

See [Destroying Namespaces](managing-namespaces.md#destroying-namespaces) or [Disabling Namespaces](managing-namespaces.md#disabling-namespaces) for more information.

4\) Disable the regions used by the NVDIMM \(nmem\) that needs to be disabled

```text
# ndctl disable-region <region.X>
```

See [Disabling Regions](managing-regions.md#disabling-regions) for more information.

5\) Disable a single, subset, or all NVDIMM \(nmem\) devices

To disable a single NVDIMM, use:

```text
# ndctl disable-dimm nmem0
disabled 1 nmem
```

To disable a subset or specific list or NVDIMMs, use:

```text
# ndctl disable-dimm nmem0 nmem1 nmem5
disabled 3 nmem
```

To disable all NVDIMMs, use:

```text
# ndctl disable-dimm all
disabled 12 nmem
```

6\) Verify the NVDIMM\(s\) are disabled by listing inactive dimms and verifying the 'state':

```text
# ndctl list -Di
{
  "dev":"nmem0",
  "id":"8089-a2-1809-00000107",
  "handle":1,
  "phys_id":29,
  "state":"disabled"
}
...
```

## Enabling NVDIMMs

1\) Verify the nmem device, or list of nmem devices, that need to be enabled using the `ndctl list -Di` command:

```text
# ndctl list -Di
{
  "dev":"nmem0",
  "id":"8089-a2-1809-00000107",
  "handle":1,
  "phys_id":29,
  "state":"disabled"
}
```

2\) Enable the NVDIMM\(s\)

To enable a single NVDIMM \(nmemX\) device, use:

```text
# ndctl enable-dimm nmem0
enabled 1 nmem
```

To enable a subset of disabled NVDIMMs, use:

```text
# ndctl enable-dimm nmem0 nmem1 nmem5
enabled 3 nmem
```

To enable all disabled NVDIMMs, use:

```text
# ndctl enable-dimm all
enabled 12 nmem
```

3\) Verify the state by listing all NVDIMMs

```text
# ndctl list -Di
```

A filtered list of NVDIMMs can shown using the `-d <nmemX>` or `-dimm <nmemX>` option, eg:

```text
# ndctl list -Di -d nmem0
- or -
# ndctl list -Di -dimm nmem0
```

## Sanitize NVDIMMs

Sanitizing one or more NVDIMMs perform a cryptographic destruction or overwrite of the contents of the given NVDIMM\(s\).  The sanitize-dimm command performs a cryptographic destruction of the contents of the given NVDIMM. It scrambles the data, and any metadata or info-blocks, but it doesn’t modify namespace labels. Therefore, any namespaces on regions associated with the given NVDIMM will be retained, but they will end up in the raw mode.

Additionally, after completion of this command, the security and passphrase for the given NVDIMM will be disabled, and the passphrase and any key material will also be removed from the keyring and the ndctl keys directory at /etc/ndctl/keys.

The command supports two different methods of performing the cryptographic erase. The default is crypto-erase, but additionally, an overwrite option is available which overwrites not only the data area, but also the label area, thus losing record of any namespaces the given NVDIMM participates in.

{% hint style="info" %}
Sanitizing NVDIMMs requires the region to be disabled first. If there are existing namespaces, those too must be destroyed or disabled. See the [Managing Regions](managing-regions.md) section for more information.
{% endhint %}

### Examples

Sanitize a single NVDIMM. This requires the region is disabled. The following destroys all namespaces, disables the region, the sanitizes the DIMMs within the region.

1\) Stop all applications that use a namespace associated with the NVDIMMs that need to be sanitized.

2\) Unmount any mounted file systems

```text
$ sudo umount <mountpoint>
```

3\) Destroy the namespaces

```text
$ sudo ndctl destroy-namespace --force [all | --region X]
```

4\) Identify the NVDIMMs associated with the region using the `ndctl list -Rvv` or `ndctl list -DR` command. `-D` displays DIMMs, `-R` displays regions. The JSON formatted output shows the hierarchy.

```text
$ sudo ndctl list -DR
{
...
  "regions":[
    {
      "dev":"region1",
      "size":1623497637888,
      "available_size":0,
      "max_available_extent":0,
      "type":"pmem",
      "iset_id":-2506113243053544244,
      "mappings":[
        {
          "dimm":"nmem11",
          "offset":268435456,
          "length":270582939648,
          "position":5
        },
        {
          "dimm":"nmem10",
          "offset":268435456,
          "length":270582939648,
          "position":1
        },
        {
          "dimm":"nmem9",
          "offset":268435456,
          "length":270582939648,
          "position":3
        },
        {
          "dimm":"nmem8",
          "offset":268435456,
          "length":270582939648,
          "position":2
        },
        {
          "dimm":"nmem7",
          "offset":268435456,
          "length":270582939648,
          "position":4
        },
        {
          "dimm":"nmem6",
          "offset":268435456,
          "length":270582939648,
          "position":0
        }
      ],
      "persistence_domain":"memory_controller"
    },
    {
      "dev":"region0",
      "size":1623497637888,
      "available_size":1597727834112,
      "max_available_extent":1597727834112,
      "type":"pmem",
      "iset_id":3259620181632232652,
      "mappings":[
        {
          "dimm":"nmem5",
          "offset":268435456,
          "length":270582939648,
          "position":5
        },
        {
          "dimm":"nmem4",
          "offset":268435456,
          "length":270582939648,
          "position":1
        },
        {
          "dimm":"nmem3",
          "offset":268435456,
          "length":270582939648,
          "position":3
        },
        {
          "dimm":"nmem2",
          "offset":268435456,
          "length":270582939648,
          "position":2
        },
        {
          "dimm":"nmem1",
          "offset":268435456,
          "length":270582939648,
          "position":4
        },
        {
          "dimm":"nmem0",
          "offset":268435456,
          "length":270582939648,
          "position":0
        }
      ],
      "persistence_domain":"memory_controller"
    }
  ]
}

```

5\) Disable the region\(s\)

```text
$ sudo ndctl disable-region 1
disabled 1 region
```

6\) Sanitize the DIMM\(s\) associated with the region\(s\) using the overwrite \(`-o`\) procedure. The -`c` \(cryptographic\) option works on DIMMs that were previously encrypted.

```text
$ sudo ndctl sanitize-dimm -o nmem6 nmem7 nmem8 nmem9 nmem10 nmem11
overwrite issued for 6 nmems.
```

{% hint style="info" %}
Note: If the DIMMs were not encrypted with a passphrase, you may see harmless messages such as the following for each DIMM

```text
failed to open file /etc/ndctl/keys/nvdimm_8089-a2-1837-00000e88_{hostname}.blob: No such file or directory
```
{% endhint %}

7\) You may need to re-provision the NVDIMMs using the vendors utility. For example, use [ipmctl ](https://docs.pmem.io/ipmctl-user-guide/)for Intel Optane DC Persistent Memory to recreate the goal. Then use `ndctl` to [create the namespace configuration](managing-namespaces.md).

