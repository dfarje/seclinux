+++
title = "Bindcompilation"
date = "2024-03-31T19:30:20Z"
author = "David Farje"
authorTwitter = "" #do not include @
cover = ""
tags = ["bind", "compilation", "named"]
keywords = ["bind9", "compilation"]
description = "In this article describe the process of compiling bind 9.18.21 from source"
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++


# Bind Stable Compilation
In this article I will document the process of compiling ISC Bind 9.18.21 from source on a Rocky Linux 8 minimal install host.

In order to compile Bind 9.18.21 on Rocky Linux minimal install host you must first install many dependencies.  You must first install a C compiler and the gnu autotools.  The rest of the dependencies may be installed from Rocky package repository but some must be installed and compiled from source.

The dependecies are the following

- libuv
- liburcu
- libxml2
- libnghttp2
- json-c
- lmdb
- protobuf-c
- fstrm-devel

These dependencies are required when compiling Bind the following way

```shell

$ ./configure --prefix=/opt/bind9 --enable-developer --enable-warn-error --enable-dnstap --enable-singletrace --enable-querytrace --enable-full-report --with-lmdb --with-libxml2 --with-json-c --disable-fips-mode --with-libnghttp2  --enable-fixed-rrset

```

## Installing libuv

