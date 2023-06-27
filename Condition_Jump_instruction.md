## Condition Jump instruction

有一类用于条件判断分支转移的指令能实现与高级语言中if语句相似的作用

```assembly
beq x1, x2, L1
```

意思是如果x1与x2相等则跳转到指令目标地址L1处，否则顺序执行下面的指令语句

beq是相等跳转，bne是不等跳转，blt是小于跳转，bltu是无符号小于跳转，bge是大于等于跳转

jump(j)指令是无条件分支转移指令，直接跳转到指令目标地址

C code:

```c
if(i == j)
    a = b + c;
```

in ASM:

```assembly
bne x13, x14, exit
add x10, x11, x12
exit:
```

如果是更为复杂的if-else语句

C code:

```c
if(i == j)
    a = b + c;
else
    a = b - c;
```

in ASM:

```assembly
bne x13, x14, else
add x10, x11, x12
j exit
else:	sub x10, x11, x12
exit:
```

以及更为复杂的for循环

C code:

```c
int a[20];
int i;
for(i = 0;i<20;i++)
    a[i] = i;
```

in ASM:

```assembly
add x9, x15, x0		#x9 = &a[0]
add x13, x0, x0		#x13 = i = 0
addi x10, x0, 20	#x10 = 20
loop:
bge x13, x10, exit	#大于等于跳转
sw x13, 0(x9)		#a[i] = i
addi x9, x9, 4		#&a[i+1]
addi x13, x13, 1	#i = i + 1
j loop
exit:
...
```

