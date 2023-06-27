## Logical Instruction



- **AND	与运算**

Register:

```assembly
and x5, x6, x7		#	x5 = x6 & x7
```

Immediate:

```assembly
andi x5, x6, 3		#	x5 = x6 & 3
```

立即数型可以用来进行掩码操作

```assembly
addi x5, x6, 0x000000ff
```

用来获取最低位的一个字节

```assembly
addi x5, x6, 0xff000000
```

用来获取最高位的一个字节

- **NOT	取反**

**RISC-V中没有专门的not指令来取反**，而是用xori指令与立即数-1来取反

- **SLL	SRL	逻辑左移与逻辑右移**

**逻辑左移=算数左移**，每次移动，右边(最低位)补0，因此RISC-V中只有逻辑左移

```assembly
slli x11, x12, 2		#	x11 = x12 << 2(C code)
```

**逻辑右移与算数右移不同**，不管符号位,左边统一补0

```assembly
addi x10, x0, 0x34ff	#	x10 = 0x0000_34ff
slli x12, x10, 0x10		#	x12 = 0x34ff_0000
srli x12, x12, 0x08		#	x12 = 0x0034_ff00
and	 x12, x12, x10		#	x12 = 0x0000_3400
```

以此操作即可得到掩码的值

- **SRA	算数右移**

当对操作数执行算数右移n位后空出的高位由原数最高比特位的符号扩展得到

```assembly
srai x10, x10, 4
```

32'b1111_1111_1111_1111_1111_1111_1110_0111 = -25

变成:

32'b1111_1111_1111_1111_1111_1111_1111_1110 = -2

如果算数右移，右移n位后，由于丢失了原数的低比特数据，**因此得到的结果不等同于原数除以2的n次方**

Arithmetic : add, addi, sub

Logical : sll, srl, slli, srli, sra, srai, and, or, xor, andi, ori, xori

RISC-V中没有立即数减指令，可以通过立即数加指令完成