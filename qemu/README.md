# NOTE

## Run RISC-V Distro/Image

I'm following this page: https://wiki.qemu.org/Documentation/Platforms/RISCV


Download linux distro image
```
wget https://dl.fedoraproject.org/pub/alt/risc-v/repo/virt-builder-images/images/Fedora-Minimal-Rawhide-20200108.n.0-fw_payload-uboot-qemu-virt-smode.elf
```

Disk Image
```
wget https://dl.fedoraproject.org/pub/alt/risc-v/repo/virt-builder-images/images/Fedora-Minimal-Rawhide-20200108.n.0-sda.raw.xz
unxz Fedora-Minimal-Rawhide-20200108.n.0-sda.raw.xz
```

Then `run.sh`

```
Login: riscv
Password: fedora_rocks!
```

## Misc

So qemue already supports quite some risc-v machine/board models.
Each model would have its own IO devices and setup.

QEMU really has a great design, adding a new machine/board model is so simple.
I suppose it is just define a set of memory map, and a few other things.

```
qemu-system-riscv64 -machine help                        
Supported machines are:
none                 empty machine
sifive_e             RISC-V Board compatible with SiFive E SDK
sifive_u             RISC-V Board compatible with SiFive U SDK
spike                RISC-V Spike Board (default)
spike_v1.10          RISC-V Spike Board (Privileged ISA v1.10)
spike_v1.9.1         RISC-V Spike Board (Privileged ISA v1.9.1)
virt                 RISC-V VirtIO board
```

## QEMU Code Study

I'm using my old code study repo.

So the riscv machine model related code is in `hw/riscv/*`.
It says how each model is defined, e.g., `sifive_e.c` file has an array of its I/O devices and their MMIO address range. And some setup.

I'm curious how normal RISC-V instructions are simulated/handled.

Ok, it is in `target/riscv`. All arch inst stuff are here.

Then it is totally possible we simply change QEMU to get the effect we wanted.
But how trustworthy can this approach be?

### PMP

https://github.com/lastweek/source-qemu/blob/master/src/target/riscv/pmp.c

`target/riscv/pmp.c` physical memory protection. This file simulates PMP's behavior.


How it interleaves with binary translation?

### Firmware

So the default firmware in QEMU + RISCV is the OpenSBI.
