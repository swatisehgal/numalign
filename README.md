# numalign - a simple tool to check resource alignment.

`numalign` tells you if a set of resources is aligned on the same NUMA node. That's it.

## license
numalign (C) 2020 Red Hat Inc and licensed under the Apache License v2

## build
just run
```bash
make
```

## Container image
coming soon

## Example output
From a developer laptop:
```
$ ./numalign 
$
$ # no output, let's see why
$ NUMALIGN_DEBUG=1 ./numalign
2020/01/24 14:00:41 CPU: allowed: [0 1 2 3]
2020/01/24 14:00:41 CPU: NUMA node by id: map[0:0 1:0 2:0 3:0]
2020/01/24 14:00:41 No PCI devices detected
$
$ # OK, let's skip the PCI device check 
$ NUMALIGN_SKIP_CHECK_PCIDEVS=1 ./numalign
STATUS ALIGNED=true
NUMA NODE=0
^C
$
$ NUMALIGN_SKIP_CHECK_PCIDEVS=1 NUMALIGN_DEBUG=1 ./numalign 
2020/01/24 14:00:58 CPU: allowed: [0 1 2 3]
2020/01/24 14:00:58 CPU: NUMA node by id: map[0:0 1:0 2:0 3:0]
STATUS ALIGNED=true
NUMA NODE=0
^C
$
$ # but what about some PCI devs?
$ export PCIDEVICE_FOOBAR="0000:3c:00.0"
$ # past the PCIDEVICE_ prefix, the rest of the variable name is not really important
$ NUMALIGN_DEBUG=1 ./numalign 
2020/01/24 14:02:50 CPU: allowed: [0 1 2 3]
2020/01/24 14:02:50 CPU: NUMA node by id: map[0:0 1:0 2:0 3:0]
2020/01/24 14:02:50 PCI: devices: 0000:3c:00.0
STATUS ALIGNED=true
NUMA NODE=0
^C

```
