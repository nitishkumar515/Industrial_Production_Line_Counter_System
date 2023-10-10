# Industrial_Production_Line_Counter_System
## Introduction 

In this project, I aim to Design and build a Production Line Counter System  using smart sensor to fully embrace automation. The method uses Industrial Automation systems and smart sensors to maintain and bring the accuracy over counting. This methodology can be implemented in any Industry. This method is cost efficient and can be easily implemented. I am implementing this all on riscv processor rather than arduino board.

## Advantages
1. The Number Counting System brings more accuracy over counting.
2. More efficient.
3. Cost implementation is less.
4. Reduces man power over the industries.
5. Automated Tireless counting.
6. No Error probability in counting.
7. Keep Count Data Stored as well as Display live count.

## Uses
1. Detecting objects on the roller conveyer.
2. Detecting cartons on the conveyer.
3. Counting screws.
4. Detecting engine block on the conveyer.
5. Detecting body in the coating process.
6. Detecting PC board.
7. Counting wafers.
8. Detecting pizza dough.
## Requirements

Here I am using *Z3R-400* Standard retro-reflective sensor. The small beam of the Z3R-400 sensor allows for detecting or counting product flowing through a a process with narrow spaces. The sensor can detect the interruption to a reflected light beam, and decide if an object is present or not.
### Sensor

![senso](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/141af6b3-3514-4de2-8863-4a59784917e2)



## Block Diagram
![blo](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/8e505ea4-a3b2-4001-a0fc-fe4a352251a0)




## C Code
```
#include<stdio.h>
int sensor_output_pin=0;
int reset_pin=0;
int count=0;
int main ()
{
while(1)
    {
        if(reset_pin == 1)
        {
            count = 0;
        }
        else if (sensor_output_pin == 1)
        {
            count++;
    }
   
}
return 0;
}


```

## Assembly code conversion

Compile the c program using RISCV-V GNU Toolchain and dump the assembly code into water_level_assembly.txt using the below commands.
```
/home/nitish/riscv32-toolchain/bin/riscv32-unkown-elf-gcc -march=rv32i -mabi=ilp32 -ffreestanding -o ./plcount.o  plcount.c
/home/nitish/riscv32-toolchain/bin/riscv32-unknown-elf-objdump -d  plcount.o > plcount.txt
```
```
p_line_count.o:     file format elf32-littleriscv


Disassembly of section .text:

00010094 <main>:
   10094:	ff010113          	add	sp,sp,-16
   10098:	00812623          	sw	s0,12(sp)
   1009c:	01010413          	add	s0,sp,16
   100a0:	000117b7          	lui	a5,0x11
   100a4:	0dc7a703          	lw	a4,220(a5) # 110dc <reset_pin>
   100a8:	00100793          	li	a5,1
   100ac:	00f71663          	bne	a4,a5,100b8 <main+0x24>
   100b0:	8001a423          	sw	zero,-2040(gp) # 110e0 <count>
   100b4:	fedff06f          	j	100a0 <main+0xc>
   100b8:	000117b7          	lui	a5,0x11
   100bc:	0d87a703          	lw	a4,216(a5) # 110d8 <__DATA_BEGIN__>
   100c0:	00100793          	li	a5,1
   100c4:	fcf71ee3          	bne	a4,a5,100a0 <main+0xc>
   100c8:	8081a783          	lw	a5,-2040(gp) # 110e0 <count>
   100cc:	00178713          	add	a4,a5,1
   100d0:	80e1a423          	sw	a4,-2040(gp) # 110e0 <count>
   100d4:	fcdff06f          	j	100a0 <main+0xc>

```

* Number of different instructions: 7
* List of unique instructions
```
j
lui
lw
li
sw
add
bne

```

## Word of Thanks
I sciencerly thank **Mr. Kunal Gosh**(Founder/**VSD**) for helping me out to complete this flow smoothly.

## Acknowledgement
- Kunal Ghosh, VSD Corp. Pvt. Ltd.
- Skywater Foundry
- Mayank Kabra,imtech
- Bhargav DV,MS
  
## Reference 

- https://github.com/The-OpenROAD-Project/OpenSTA.git
- https://github.com/kunalg123
- https://www.vsdiat.com
- https://github.com/SakethGajawada/RISCV-GNU
