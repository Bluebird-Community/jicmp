[![jicmp-build](https://github.com/Bluebird-Community/jicmp/actions/workflows/jicmp-build.yaml/badge.svg)](https://github.com/Bluebird-Community/jicmp/actions/workflows/jicmp-build.yaml)

# About JICMP

_JICMP_ is a small library to allow the use of _IPv4_ _ICMP_ (raw) packets in Java.

## Build from source

Requirements:

* git
* automake
* autoconf
* libtool
* Java JDK 1.8+

The repository has a _git_ submodule which contains _Macros_ required to compile from source code.

Clone the respository on local disk

```bash
git clone https://github.com/OpenNMS/jicmp.git
```

.Switch into source code repository
```bash
cd jicmp
```

.Initialize and update the git submodule.
```bash
git submodule update --init --recursive
```

.Update generated configuration files with
```bash
autoreconf -fvi
```

.Generate make files using `/usr/local/lib` as install path and compile JICMP
```bash
./configure
make
```

> [!TIP]
> If you want to change the install path the `./configure --prefix=/your/custom/path` can be used.

.Install the library on your system, root permissions may required when working as non-root user.
```bash
sudo make install
```
## Using JICMP as non-root

_Mac OS X_ supports non-root _ICMP_ through the _$$SOCK_DGRAM$$_ interface, which _JICMP_ uses by default.

_Linux_ supports this as well, but you additionally need to set a sysctl _OID_ to allow ping for non-root users.

You can set this temporarily by running: 
 
```bash
sysctl -w net.ipv4.ping_group_range="0 429496729"
```

... or by creating a `sysctl` configuration file in `/etc`:

```bash
echo "net.ipv4.ping_group_range=0 429496729" > /etc/sysctl.d/03-non-root-icmp.conf
```
