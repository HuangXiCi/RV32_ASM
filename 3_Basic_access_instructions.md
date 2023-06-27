## Basic access instructions



计算机系统中不同格式的数据有的会低于32位，但是很少低于8位，因此以8位作为单位数据，以8位的倍数来存储数据

- Big Endian	

大端是将一个字数据的最低位字节存储在最高字节地址上

| ADDR3 | ADDR2 | ADDR1 | ADDR0 |
| ----- | ----- | ----- | ----- |
| BYTE0 | BYTE1 | BYTE2 | BYTE3 |

- Little Endian

小端是将一个字数据的最低位字节存储在最低字节地址上

| ADDR3 | ADDR2 | ADDR1 | ADDR0 |
| ----- | ----- | ----- | ----- |
| BYTE3 | BYTE2 | BYTE1 | BYTE0 |

在RISC-V的存储系统中，是以字节为单位来寻址的

每个字地址可以拆分到4个字节地址，在小端系统中某个字的地址与它的最低位字节地址是相同的



- So how to Load from Memory to Register

C code:

```c
int a[5] = {1,2,3,4,5};
c = b + a[3];
```

Using Load Word (lw) in RISC-V:

```assembly
lw x10, 12(x15)		#Reg x10 gets a[3]
add x11, x12, x10
```

其中：x15 是 a[0] 的指针

而12是字节的偏移量(offset in bytes) ， 一个int变量占4个字节



- Store from Register to Memory

C code:

```c
int a[5] = {1,2,3,4,5};
a[4] = b + a[3];
```

Using Store Word (sw) in RISC-V:

```assembly
lw x10, 12(x15)		#Reg x10 gets a[3]
add x11, x12, x10
sw x10, 16(x15) 	#Mem a[4] gets x10
```



同时，RISC-V还提供了读字节数据和写字节数据

RISC-V提供字节数据的访存传输指令lb和sb，它们的指令格式与lw ， sw相同，但只针对1个字节的源数据进行操作

sb时，将寄存器中最低字节的1字节数据保存到对应的字节地址中

lb时，将字节地址中的1字节数据经过符号位扩展后装载到对应寄存器中

同时，还有无符号扩展指令lbu，全部扩展0后装载到对应的寄存器中

注意：RISC-V中没有sbu
