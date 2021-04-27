# Installing NDCTL and DAXCTL from Source on Linux

These instructions provide a step-by-step guide for installing the `ndctl` and `daxctl` utilities from the GitHub project [master branch](https://github.com/pmem/ndctl).

### 1. Install the Prerequisites

There are a number of packages required for the build steps that may not be installed by default. For information about the required packages, see the "BuildRequires:" lines in ndctl.spec.in.

[https://github.com/pmem/ndctl/blob/master/ndctl.spec.in](https://github.com/pmem/ndctl/blob/master/ndctl.spec.in)

To successfully compile ndctl and daxctl from source with documentation, the following packages are required

* autoconf 
* automake 
* asciidoc \(asciidoctor\)
* bash-completion
* doxygen 
* gcc 
* gcc-c++ \(g++\)
* git
* glib2 
* glib2-devel 
* graphviz 
* json-c-devel
* keyutils-libs-devel \(libkeyutils-dev\[el\]\)
* kmod 
* kmod-devel 
* libfabric 
* libfabric-devel 
* libtool 
* libudev-devel 
* libuuid-devel
* ncurses 
* pandoc 
* pkg-config 
* rubygem-asciidoctor \(asciidoctor\)
* xmlto

To install these prerequisites, use:

{% tabs %}
{% tab title="Fedora" %}
Fedora 21 or earlier

```text
sudo yum install git gcc gcc-c++ autoconf automake asciidoc asciidoctor xmlto libtool pkg-config glib2 glib2-devel libfabric libfabric-devel doxygen graphviz pandoc ncurses kmod kmod-devel libudev-devel libuuid-devel json-c-devel keyutils-libs-devel
```

Fedora 22 or later

```text
sudo dnf install git gcc gcc-c++ autoconf automake asciidoc asciidoctor xmlto libtool pkg-config glib2 glib2-devel libfabric libfabric-devel doxygen graphviz pandoc ncurses kmod kmod-devel libudev-devel libuuid-devel json-c-devel keyutils-libs-devel
```
{% endtab %}

{% tab title="RHEL & CentOS" %}
These instructions apply to RHEL, CentOS, and RHEL for SAP HANA v7.6 or later.

Some of the required packages can be found in the EPEL repository \(Extra Packages for Enterprise Linux\). 

Verify the EPEL repository is available and active:

```text
yum repolist
```

Example:

```text
$ yum repolist
repo id                                                       repo name                                      status
epel/x86_64                                                   Extra Packages for Enterprise Linux 7 - x86_64 13,217
```

If the EPEL repository is not listed, install and activate it using:

```text
sudo yum install epel-release
```

Install the required packages

```text
sudo yum install git gcc gcc-c++ autoconf automake asciidoc bash-completion xmlto libtool pkgconfig glib2 glib2-devel libfabric libfabric-devel doxygen graphviz pandoc ncurses kmod kmod-devel libudev-devel libuuid-devel json-c-devel rubygem-asciidoctor keyutils-libs-devel
```
{% endtab %}

{% tab title="Ubuntu & Debian" %}
**For Ununtu 18.04 \(Bionic\) and Debian 9 \(Stretch\) or later:**

```text
sudo apt install -y git gcc g++ autoconf automake asciidoc asciidoctor bash-completion xmlto libtool pkg-config libglib2.0-0 libglib2.0-dev libfabric1 libfabric-dev doxygen graphviz pandoc libncurses5 libkmod2 libkmod-dev libudev-dev uuid-dev libjson-c-dev libkeyutils-dev
```

**For Ubuntu 16.04 \(Xenial\) and Debian 8 \(Jessie\):**

{% hint style="info" %}
Earlier releases of Ubuntu and Debian do not have libfabric1 or libfabric-dev available in the repository. If these libraries are required, you should compile them yourself. See [https://github.com/ofiwg/libfabric](https://github.com/ofiwg/libfabric)
{% endhint %}

```text
sudo apt-get install -y git gcc g++ autoconf automake asciidoc asciidoctor bash-completion xmlto libtool pkg-config libglib2.0-0 libglib2.0-dev doxygen graphviz pandoc libncurses5 libkmod2 libkmod-dev libudev-dev uuid-dev libjson-c-dev libkeyutils-dev
```
{% endtab %}

{% tab title="SLES & OpenSUSE" %}
These instructions were tested on OpenSUSE/SLES 12sp5, 15sp2, and OpenSUSE Leap15.2

```text
sudo zypper install git gcc gcc-c++ autoconf automake asciidoc xmlto libtool pkg-config glib2 glib2-devel libfabric libfabric-devel doxygen graphviz pandoc ncurses kmod libkmod-devel libudev-devel libuuid-devel libjson-c-devel keyutils-devel
```

Install asciiddoctor using the gem utility

```text
sudo gem install asciidoctor
```
{% endtab %}
{% endtabs %}

### 2. Clone the GitHub Repository

2.1\) If you're behind a company proxy, configure git to work with your proxy server first. The following configures a HTTP and HTTPS proxy for all users. Refer to the [git-config documentation](https://git-scm.com/docs/git-config) for more options and information.

```text
git config --global http.proxy http://proxyUsername:proxyPassword@proxy.server.com:port
git config --global https.proxy https://proxyUsername:proxyPassword@proxy.server.com:port
```

2.2\) Create a working directory to clone the ndctl GitHub repository to, eg: 'downloads'

```text
mkdir ~/downloads
```

2.3\) Clone the repository:

```text
cd ~/downloads
git clone https://github.com/pmem/ndctl
cd ndctl
```

### 3. Build

The following configures ndctl to be installed in to the /usr/local directory.

```text
./autogen.sh
./configure CFLAGS='-g -O2' --prefix=/usr/local --sysconfdir=/etc --libdir=/usr/local/lib64
make
```

For a full list of configure options use:

```text
./configure --help
```

#### **Build using an alternative compiler**

**Note:** If you want to compile with a different compiler other than gcc, you have to provide the CC and CXX environment variables. For example:

```text
make CC=clang CXX=clang++
```

These variables are independent and setting CC=clang does not set CXX=clang++.

#### Build a Debug Version

To compile ndctl with debugging, use the `--enable-debug` option:

```text
./autogen.sh
./configure CFLAGS='-g -O2' --enable-debug --prefix=/usr/local --sysconfdir=/etc --libdir=/usr/local/lib64
make
```

The ndctl code uses many statically defined functions which the compiler will optimize as inline assembly ****when referenced only once. This means the function name is removed from the ELF symbol table and tools such as gdb, ltrace, or bpftrace cannot show this information. It can make it more difficult to understand code flow or troubleshoot issues. Use the `-fno-inline -g3 -O0` options to compile ndctl with no optimizations to make all symbols \(functions\) available for tracing, use:

```text
./autogen.sh
./configure CFLAGS='-fno-inline -g3 -O0' --enable-debug --prefix=/usr/local --sysconfdir=/etc --libdir=/usr/local/lib64
make
```

### 4. Install

Once ndctl has successfully been compiled, it can be installed using the following:

```text
sudo make install
```

### 5. Build and Run Unit Tests \(Optional\)

The unit tests run by `make check` require the nfit\_test.ko module to be loaded. To build and install nfit\_test.ko:

1. Obtain the kernel source. For example, `git clone -b libnvdimm-for-next git://git.kernel.org/pub/scm/linux/kernel/git/nvdimm/nvdimm.git`
2. Skip to step 3 if the kernel version is &gt;= v4.8. Otherwise, for kernel versions &lt; v4.8, configure the kernel to make some memory available to CMA \(contiguous memory allocator\). This will be used to emulate DAX. `CONFIG_DMA_CMA=y` `CONFIG_CMA_SIZE_MBYTES=200` **or** `cma=200M` on the kernel command line.
3. Compile the libnvdimm sub-system as a module, make sure "zone device" memory is enabled, and enable the btt, pfn, and dax features of the sub-system: `CONFIG_X86_PMEM_LEGACY=m` `CONFIG_ZONE_DEVICE=y` `CONFIG_LIBNVDIMM=m` `CONFIG_BLK_DEV_PMEM=m` `CONFIG_ND_BLK=m` `CONFIG_BTT=y` `CONFIG_NVDIMM_PFN=y` `CONFIG_NVDIMM_DAX=y` `CONFIG_DEV_DAX_PMEM=m`
4. Build and install the unit test enabled libnvdimm modules in the following order. The unit test modules need to be in place prior to the `depmod` that runs during the final `modules_install` `make M=tools/testing/nvdimm` `sudo make M=tools/testing/nvdimm modules_install` `sudo make modules_install`
5. Now run `make check` in the ndctl source directory, or `ndctl test`, if ndctl was built with `--enable-test`.

### Troubleshooting

The unit tests will validate that the environment is set up correctly before they try to run. If the platform is misconfigured, i.e. the unit test modules are not available, or the test versions of the modules are superseded by the "in-tree/production" version of the modules `make check` will skip tests and report a message like the following in test/test-suite.log:

```text
SKIP: libndctl
==============
test/init: nfit_test_init: nfit.ko: appears to be production version: /lib/modules/4.8.8-200.fc24.x86_64/kernel/drivers/acpi/nfit/nfit.ko.xz
__ndctl_test_skip: explicit skip test_libndctl:2684
nfit_test unavailable skipping tests
```

If the unit test modules are indeed available in the modules 'extra' directory the default depmod policy can be overridden by adding a file to /etc/depmod.d with the following contents:

```text
override nfit * extra
override device_dax * extra
override dax_pmem * extra
override libnvdimm * extra
override nd_blk * extra
override nd_btt * extra
override nd_e820 * extra
override nd_pmem * extra
```

The nfit\_test module emulates pmem with memory allocated via vmalloc\(\). One of the side effects is that this breaks 'physically contiguous' assumptions in the driver. Use the `--align=4K` option to `ndctl create-namespace` to avoid these corner case scenarios.

