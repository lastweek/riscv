# Steps

We need to specify the path to the riscv64 GCC/OBJCOPY/READELF.
We are producing risc64 binaries.

```
READELF=riscv64-linux-gnu-readelf OBJCOPY=riscv64-linux-gnu-objcopy CC=riscv64-linux-gnu-gcc ../configure --host=riscv64-unknown-el
make
```
