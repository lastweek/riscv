all:
	riscv64-linux-gnu-gcc -static -o hello hello.c

dis:
	riscv64-linux-gnu-objdump -D hello

run:
	spike pk hello
