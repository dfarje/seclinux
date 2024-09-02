+++
title = "Bindcompilation"
date = "2024-03-31T19:30:20Z"
author = "David Farje"
authorTwitter = "" #do not include @
cover = ""
tags = ["bind", "compilation", "named"]
keywords = ["bind9", "compilation"]
description = "In this article describe the process of compiling bind 9.20.1 from source"
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++


# Bind New Stable Compilation
In this article I will document the process of compiling the new stable ISC BIND 9.20.01 from source on a Rocky Linux 8 minimal install host.

In order to compile BIND 9.20.01 on Rocky Linux minimal you must first install a C compiler and make.

The following dependencies must be also installed.

- libuv (Async I/O)
- libcap (capabilities)
- liburcu (Userspace RCU for concurrency)
- jemalloc (Efficient memory allocator from FreeBSD project)
- libxml2 (XML Stats Channel)
- libnghttp2 (To support DoH)
- json-c (JSON stat interface)
- lmdb (in memory datastore)
- protobuf-c (to support DNSTAP)
- fstrm-devel (to support DNSTAP)
- cmocka  (for unit testing)



#### 1. Get BIND source code

To get the new stable BIND source code 

```shell
curl https://downloads.isc.org/isc/bind9/9.20.1/bind-9.20.1.tar.xz -o bind-9.20.1.tar.xz
```

#### 2. Install gcc and GNU/Autotools

To install the GCC compiler and GNU/Autotools is possible to install each utility one by one.  However it will be tedius and error/time prone.  To install these dependencies install development package group for Redhat.

```shell

sudo dnf -y install gcc gcc-c++ make bzip2 tar perl

```

#### 3. Enable devel repo and epel repo

To compile BIND you will need many devel packages.  To install these packages you will need access to the devel repo.
To enable devel repo


```shell
sudo dnf config-manager --enable devel
```

```shell
sudo dnf -y install epel-release
```

#### 4. Installing liburcu

The liburcu library provides RCU functionality in user space.  RCU is used by BIND to achieve thread concurrency.  RCU functionality is implemented in the Linux kernel but bind uses a user space implementation.

If you want to learn more about RCU check this link:

[What is RCU, Fundamentally?](https://lwn.net/Articles/262464/).

To install librcu on Rocky 8 for the purposes of compiling BIND you will have to download and install from source.


Install URCU development files


```shell
sudo dnf -y install userspace-rcu-devel
```

#### 5. Installing libuv

The libuv library is very important in Bind since it provides the Async I/O capabilities that enable it to answer queries in parallel.

To install the libuv library in Rocky Linux 8 you can use packages or from source.

To install package

```shell
sudo dnf -y install libuv-devel
```

#### 6. Install libnghttp2

In order to support DoH, BIND will require development files from libnghttp2

```shell
sudo dnf -y install libnghttp2-devel
```


#### 7. Install OpenSSL libraries

In order for BIND to support SSL you must install SSL library development files.
The following package will provide them.


```shell
sudo dnf -y install openssl-devel
```

#### 8. Install LMDB libraries

LMDB provides a fast in memory database for BIND to use. To use this library you must
install the following package.


```shell
sudo dnf -y install lmdb-devel
```


#### 9. Install libxml2 libraries

BIND is able to send statistics channel via XML.  To do this it requires libxml2 libraries.
You may install libxml2 libraries on Rocky 8 as follows:

```shell
sudo dnf -y install libxml2-devel
```

#### 10. Install json-c libraries

BIND is also able to provide statistics via JSON format.  It will require the json-c libraries.
To install use the following command

```shell
sudo dnf -y install json-c-devel
```

#### 11. Install kernel capabilities library.

BIND requests kernel capabilities in order to operate securely.

```shell
sudo dnf -y install libcap-devel
```

#### 12. Install frame streaming library (fstrm) and protobuf

BIND supports dnstap.  To support this it requires frame streaming library and google's protocol buffers
To install use the command.

```shell
sudo dnf -y install fstrm-devel protobuf-c-devel
```

#### 13. Install cmocka test library

To install cmocka mock testing library use the following

```shell
sudo dnf -y install libcmocka-devel
```

#### 14. Install jemalloc memory allocator

```shell
sudo dnf -y install jemalloc-devel
```


#### 14. Compile BIND

First untar source package.

```shell
tar Jxvf bind-9.20.1.tar.xz
```

Enter the project directory

```shell
cd bind-9.20.1
```

For testing purposes I will be configuring the build as follows.

```shell
./configure --prefix=/home/david/bind9201 --enable-developer --enable-warn-error --enable-dnstap --enable-singletrace --enable-querytrace --enable-full-report --with-lmdb --with-libxml2 --with-json-c --disable-fips-mode --with-libnghttp2  --enable-fixed-rrset --with-jemalloc

```

Then make.

```shell
make
```

Finally install it

```shell
make install
```

