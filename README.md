# etc_services

[![Build Status](https://travis-ci.com/ccin2p3/puppet-etc_services.png?branch=master)](https://travis-ci.com/ccin2p3/puppet-etc_services) [![Version](https://img.shields.io/puppetforge/v/ccin2p3/etc_services.svg)](https://forge.puppet.com/ccin2p3/etc_services)

#### Table of Contents

1. [Overview](#overview)
2. [Module Description - What the module does and why it is useful](#module-description)
3. [Setup - The basics of getting started with etc_services](#setup)
    * [What etc_services affects](#what-etc_services-affects)
    * [Setup requirements](#setup-requirements)
4. [Usage - Configuration options and additional functionality](#usage)
5. [Limitations - OS compatibility, etc.](#limitations)
6. [Development - Guide for contributing to the module](#development)
7. [Contributors](#contributors)

## Overview

Adds a defined type which can manage a specific service name in `/etc/services`.

## Module Description

This module allows easy creation and removal of etc services entries via a new defined type. Each instance 

## Setup

### What etc_services affects

Entries in the `/etc/services` file.

### Setup Requirements

Just declare an instance.

## Usage

The `etc_services` defined type allows a service to be instantiated with one or more port/protocol combinations.

```puppet
etc_services { 'kerberos':
  protocols => { 'udp' => '88' },
  aliases   => [ 'kerberos5', 'krb5', 'kerberos-sec' ],
  comment   => 'Kerberos v5',
}
```

The example above will generate a single entry in `/etc/services` similar to the following:

```
kerberos  88/udp  kerberos5 krb5 kerberos-sec # Kerberos v5
```

Note that the aliases and comment are entirely optional

### Conversion from 1.x.x Releases

Starting at release 2.0.0 the syntax of each etc_services entry changed subtly. Instead of encoding the protocol in the resource name, the `port` parameter has been replaced with a hash of `protocols`. This allows a service to be defined for two ports using the same resource.

**Version < 2.0.0**

```puppet
etc_services { 'printer\tcp':
  port    => '515',
  aliases => [ 'spooler' ],
  comment => 'line printer spooler',
}

etc_services { 'printer\udp':
  port    => '515',
  aliases => [ 'spooler' ],
  comment => 'line printer spooler',
}
```

**Version >= 2.0.0**

```puppet
etc_services { 'printer':
  protocol => { 'tcp' => '515', 'udp' => '515' },
  aliases  => [ 'spooler' ],
  comment  => 'line printer spooler',
}
```

## Limitations

* This module could be used on any operating systems that has support for augeas and use the `/etc/services` file.
* Only TCP and UDP protocols are supported!

## Development

If you want to contribute or adjust some of the settings / behavior, either:
* create a new _Pull Request_.

## Contributors

Check out the [contributor list](https://github.com/ccin2p3/puppet-etc_services/graphs/contributors).
