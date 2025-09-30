# Minihyve - Easy per-vm jails

## Prerequisites

### Package dependencies
- vm-bhyve
- iocage

### Preparing network interfaces
Minihyve relies on `vmnet` network interfaces
being configured on the host before being passed
to the jails.

Create `vmnet` devices with ifconfig, pass them to
VMs by setting a `bhyve_options="-s ...` entry in
the vm-bhyve configuration files instead of the
vm-bhyve native configuration directives.

Do not forget to configure the host side of the
interfaces too.

## Installation

```sh
install -m 744 -o root -g wheel sbin/minihyve /usr/local/sbin
install -m 744 -o root -g wheel rc.d/minihyve /usr/local/etc/rc.d
```

## Usage
### Creating and managing VMs
Such operations are not covered by minihyve
and are to be done whichever way you did it before.

### Start a VM
```
minihyve start vm_name
```

### Stop a VM
```
minihyve stop vm_name
```

### List running VMs
```
minihyve list
```

### Send a command to a VM
```
minihyve cmd vm command arg1 arg2 ... argN
```

### Configuring VMs to start and shutdown automatically
The rc.d service file lets you automatically start
VMs at startup and stop them on system shutdown.

Set the `minihyve_autostart` configuration
variable to the space-separated list of VMs you
want to start on startup.
