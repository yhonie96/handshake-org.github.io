# Linux Install Guide

The Handshake software suite consists of a full node (`hskd`) and a light
client (`hnsd`). The full node allows users to register, update, and transfer
names, resolve names, and make blockchain payments. The light client (SPV node)
allows users to resolve names without the computing resource requirements of
running a full node.

This guide includes instructions for installing
[`hskd`](#hskd-installation-instructions) and
[`hnsd`](#hnsd-installation-instructions).

> Note: the instructions are specifically for Debian/Ubuntu. Be sure to use the
proper package manager for your OS. The BSDs and Solaris have not been tested yet,
but should work in theory.

<br/>

## `hskd` Installation Instructions
#### Install dependencies
- node.js
- git
```
$ sudo apt install nodejs git
```

#### Download and install `hskd`
```
$ git clone git@github.com:handshake-org/hskd.git
$ cd hskd
$ npm install --production
```

#### Start (on testnet)
```
$ ./hskd/bin/hskd --daemon --no-auth
```

<br/>

## `hnsd` Installation Instructions
#### Install dependencies
```
$ sudo apt install automake autoconf libtool unbound libunbound-dev
```
>Note: unbound-devel in yum

#### Download and compile `hnsd`
```
git clone git@github.com:handshake-org/hnsd.git
cd hnsd
./autogen.sh && ./configure --with-network && make
```

#### Start `hnsd`
```
sudo setcap 'cap_net_bind_service=+ep' /path/to/hnsd
./hnsd --pool-size=1 --rs-host=127.0.0.1:53
```

#### Configure nameserver settings
1. resolv.conf
```
$ echo 'nameserver 127.0.0.1' | sudo tee /etc/resolv.conf > /dev/null
```

2. Edit resolvconf.conf to match:
```
name_servers="127.0.0.1"
```