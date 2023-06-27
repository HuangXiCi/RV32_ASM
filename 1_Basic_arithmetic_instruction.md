## Basic arithmetic instruction



- Addition in Assembly

```assembly
add rd, rs1, rs2		#rd = rs1 + rs2
```

其中：add为操作符 ， rd 为目的寄存器 ， rs1和rs2为源操作数寄存器

- Subtraction in Assembly

```assembly
sub rd, rs1, rs2		#rd = rs1 - rs2
```

同样：sub为操作符 ， rd 为目的寄存器 ， rs1和rs2为源操作数寄存器

- Addition and Subtraction of Integers

So how to do the following C statement?

```c
a = b + c + d - e;
```

Break into multiple instructions

```assembly
add x10, x1, x2
add x10, x10, x3
sub x10, x10, x4
```

- Immediates

Add Immediates in C:

```c
a = b + 10;
```

Add Immediates in ASM:

```assembly
addi x3, x4, 10
```

秉承着越精简越好的基本原则，risc-v中没有立即数减的指令，而是采用加立即数的相反数来实现的：

Sub Immediates in C:

```c
a = b - 10;
```

Sub Immediates in ASM:

```assembly
addi x3, x4, -10
```

- MOV

秉承着越精简越好的基本原则，risc-v中没有MOV指令，而是采用add指令来实现的，寄存器x0通过硬连线的方式固定值为0，因此：

```assembly
mov x3, x4
```

在RISC-V中为：

```assembly
add x3, x4, x0
```

