# Installing NDCTL and DAXCTL Packages on Linux

The `ndctl` and `daxctl` utilities are available in many Linux distribution package repositories.  This approach is the easiest to use and maintain, compared with [installing ndctl from source code](installing-ndctl-from-source-on-linux.md). The daxctl utility is bundled with the ndctl packages.

{% tabs %}
{% tab title="Fedora" %}
1\) Query the repository to confirm if the ndctl package is available:

Fedora 21 or earlier

```text
yum search ndctl
```

Fedora 22 or later

```text
dnf repoquery ndctl
```

2\) Install the ndctl utility

Fedora 21 or earlier

```text
yum install ndctl
```

Fedora 22 or later

```text
dnf install ndctl
```
{% endtab %}

{% tab title="RHEL & CentOS" %}
The ndctl package is available on CentOS, RHEL, RHEL for SAP HANA 7.0 or later. 

1\) Query the repository to identify if the ndctl package is available:

```text
yum search ndctl
```

2\) Install the ndctl package

```text
yum install ndctl
```
{% endtab %}

{% tab title="SLES & OpenSUSE" %}
The ndctl package is available for OpenSUSE, SUSE Linux Enterprise Server \(SLES\), and SLES for SAP HANA v12.4 or later.

1\) Query the repository to identify if ndctl is delivered:

```text
sudo zypper search ndctl
```

Example:

```text
$ sudo zypper search ndctl

S | Name      | Summary                                                                    | Type   
--+-----------+----------------------------------------------------------------------------+--------
  | libndctl6 | Management library for "libnvdimm" subsystem devices (Non-volatile Memory) | package
  | ndctl     | Manage "libnvdimm" subsystem devices (Non-volatile Memory)                 | package
```

2\) Install the ndctl package

```text
sudo zypper install ndctl
```
{% endtab %}

{% tab title="Ubuntu" %}
The ndctl package is available on Ubuntu 18.10 \(Cosmic Cuttlefish\) or later.

1\) Query the repository to identify if the ndctl package is available using either the aptitude, apt-cache, or apt utilities

```text
aptitude search ndctl 
apt-cache search ndctl 
apt search ndctl
```

2\) Verify if the ndctl package is currently installed and check the version

```text
apt list --installed ndctl
```

3\) Install the ndctl package or update an installed package

```text
sudo apt-get install ndctl
```
{% endtab %}

{% tab title="Debian" %}
{% hint style="info" %}
The ndctl package is available on Debian 10 \(Buster\) or later. See [https://tracker.debian.org/pkg/ndctl](https://tracker.debian.org/pkg/ndctl) for up to date information.
{% endhint %}

1\) Query available versions in configured repos:

```text
apt policy ndctl
```

2\) Query the repository to identify if ndctl is available using either the aptitude, apt-cache, or apt utilities

```text
apt search ndctl
```

3\) Verify if the ndctl package is currently installed and check the version

```text
apt list --installed ndctl
```

4\) Install the ndctl package or update an installed package

```text
sudo apt install ndctl
```
{% endtab %}
{% endtabs %}

