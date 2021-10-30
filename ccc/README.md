# picorv32 

modified by ccc

## run

```
$ make -f ccc/ccc.mk
riscv64-unknown-elf-gcc -c -nostdlib -fno-builtin -mcmodel=medany -march=rv32ima -mabi=ilp32 -o firmware/start.o firmware/start.S
riscv64-unknown-elf-gcc -Os -nostdlib -fno-builtin -mcmodel=medany -march=rv32ima -mabi=ilp32 -ffreestanding -nostdlib -o firmware/firmware.elf \
        -Wl,-Bstatic,-T,firmware/sections.lds,-Map,firmware/firmware.map,--strip-debug \
        firmware/start.o firmware/irq.o firmware/print.o firmware/hello.o firmware/sieve.o firmware/stats.o  tests/mulhsu.o tests/mulh.o tests/blt.o tests/xori.o tests/j.o tests/andi.o tests/add.o tests/slti.o tests/jal.o tests/srl.o tests/lhu.o tests/ori.o tests/and.o tests/slli.o tests/sra.o tests/simple.o tests/remu.o tests/bltu.o tests/lui.o tests/sh.o tests/lb.o tests/lbu.o tests/slt.o tests/mulhu.o tests/bgeu.o tests/bne.o tests/jalr.o tests/addi.o tests/sb.o tests/auipc.o tests/beq.o tests/div.o tests/lw.o tests/rem.o tests/srli.o tests/sw.o tests/divu.o tests/mul.o tests/srai.o tests/bge.o tests/lh.o tests/sll.o tests/sub.o tests/xor.o tests/or.o  
c:/install/sifive/riscv64-unknown-elf-toolchain-10.2.0-2020.12.8/bin/../lib/gcc/riscv64-unknown-elf/10.2.0/../../../../riscv64-unknown-elf/bin/ld.exe: tests/simple.o: in function `.prname_done':
(.text+0x50): undefined reference to `simple_ret'
collect2.exe: error: ld returned 1 exit status
make: *** [ccc/ccc.mk:118: firmware/firmware.elf] Error 1
$ make -f ccc/ccc.mk
riscv64-unknown-elf-gcc -Os -nostdlib -fno-builtin -mcmodel=medany -march=rv32ima -mabi=ilp32 -ffreestanding -nostdlib -o firmware/firmware.elf \
        -Wl,-Bstatic,-T,firmware/sections.lds,-Map,firmware/firmware.map,--strip-debug \
        firmware/start.o firmware/irq.o firmware/print.o firmware/hello.o firmware/sieve.o firmware/stats.o  tests/mulhsu.o tests/mulh.o tests/blt.o tests/xori.o tests/j.o tests/andi.o tests/add.o tests/slti.o tests/jal.o tests/srl.o tests/lhu.o tests/ori.o tests/and.o tests/slli.o tests/sra.o tests/remu.o tests/bltu.o tests/lui.o tests/sh.o tests/lb.o tests/lbu.o tests/slt.o tests/mulhu.o tests/bgeu.o tests/bne.o tests/jalr.o tests/addi.o tests/sb.o tests/auipc.o tests/beq.o tests/div.o tests/lw.o tests/rem.o tests/srli.o tests/sw.o tests/divu.o tests/mul.o tests/srai.o tests/bge.o tests/lh.o tests/sll.o tests/sub.o tests/xor.o tests/or.o
chmod -x firmware/firmware.elf
riscv64-unknown-elf-objcopy -O binary firmware/firmware.elf firmware/firmware.bin
chmod -x firmware/firmware.bin
python firmware/makehex.py firmware/firmware.bin 32768 > firmware/firmware.hex
vvp -N testbench.vvp
hello world
lui..OK
auipc..OK
j..OK
jal..OK
jalr..OK
beq..OK
bne..OK
blt..OK
bge..OK
bltu..OK
bgeu..OK
lb..OK
lh..OK
lw..OK
lbu..OK
lhu..OK
sb..OK
sh..OK
sw..OK
addi..OK
slti..OK
xori..OK
ori..OK
andi..OK
slli..OK
srli..OK
srai..OK
add..OK
sub..OK
sll..OK
slt..OK
xor..OK
srl..OK
sra..OK
or..OK
and..OK
mulh..OK
mulhsu..OK
mulhu..OK
mul..OK
div..OK
divu..OK
rem..OK
remu..OK
 1st prime is 2.
 2nd prime is 3.
 3rd prime is 5.
 4th prime is 7.
 5th prime is 11.
 6th prime is 13.
 7th prime is 17.
 8th prime is 19.
 9th prime is 23.
10th prime is 29.
11th prime is 31.
12th prime is 37.
13th prime is 41.
14th prime is 43.
15th prime is 47.
16th prime is 53.
17th prime is 59.
18th prime is 61.
19th prime is 67.
20th prime is 71.
21st prime is 73.
22nd prime is 79.
23rd prime is 83.
24th prime is 89.
25th prime is 97.
26th prime is 101.
27th prime is 103.
28th prime is 107.
29th prime is 109.
30th prime is 113.
31st prime is 127.
checksum: 1772A48F OK
Cycle counter ......... 130097
Instruction counter .... 26191
CPI: 4.96
DONE

------------------------------------------------------------
EBREAK instruction at 0x000006BC
pc  000006C0    x8  00000000    x16 00000000    x24 00000000
x1  00000680    x9  00000000    x17 00000000    x25 00000000
x2  00020000    x10 20000000    x18 00000000    x26 00000000
x3  DEADBEEF    x11 075BCD15    x19 000068DC    x27 00000000
x4  DEADBEEF    x12 0000004F    x20 00000000    x28 0000000A
x5  00000002    x13 0000004E    x21 00000000    x29 00000000
x6  000000A5    x14 00000045    x22 00000000    x30 00000000
x7  00000000    x15 0000000A    x23 00000000    x31 00000000
------------------------------------------------------------
Number of fast external IRQs counted: 16
Number of slow external IRQs counted: 2
Number of timer IRQs counted: 22
TRAP after 159747 clock cycles
ALL TESTS PASSED.
testbench.v:266: $finish called at 1598570000 (1ps)
```