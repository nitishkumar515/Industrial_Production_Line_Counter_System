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
#include <stdio.h>

int count = 0;

void increment_Count()
{
 count =count + 1;
  printf("Item produced. Current count: %d\n", count);
 }

void decrement_Count()
 {
    if (count > 0)
 {
        count = count - 1;
        printf("Item removed. Current count: %d\n", count);
    }
else
{
        printf("No items to remove. Current count is zero.\n");
    }
}

void displayCount()
{
    printf("Current count: %d\n", count);
}

int main()
 {
    bool running = 1;
    int choice;

    while (running)
 {
        printf("\nProduction Line Counter System\n");
        printf("1. Produce an item\n");
        printf("2. Remove an item\n");
        printf("3. Display current count\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice)
{
            case 1:
                incrementCount();
                break;
            case 2:
                decrementCount();
                break;
            case 3:
                displayCount();
                break;
            case 4:
                running = 0;
                break;
            default:
                printf("Invalid choice. Please try again.\n");
                break;
        }
    }

    printf("Exiting the system.\n");
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

out_plll.o:     file format elf32-littleriscv


Disassembly of section .text:

00010094 <incrementCount>:
   10094:	ff010113          	add	sp,sp,-16
   10098:	00812623          	sw	s0,12(sp)
   1009c:	01010413          	add	s0,sp,16
   100a0:	000117b7          	lui	a5,0x11
   100a4:	16c7a783          	lw	a5,364(a5) # 1116c <__DATA_BEGIN__>
   100a8:	00178713          	add	a4,a5,1
   100ac:	000117b7          	lui	a5,0x11
   100b0:	16e7a623          	sw	a4,364(a5) # 1116c <__DATA_BEGIN__>
   100b4:	00000013          	nop
   100b8:	00c12403          	lw	s0,12(sp)
   100bc:	01010113          	add	sp,sp,16
   100c0:	00008067          	ret

000100c4 <displayCount>:
   100c4:	ff010113          	add	sp,sp,-16
   100c8:	00812623          	sw	s0,12(sp)
   100cc:	01010413          	add	s0,sp,16
   100d0:	00000013          	nop
   100d4:	00c12403          	lw	s0,12(sp)
   100d8:	01010113          	add	sp,sp,16
   100dc:	00008067          	ret

000100e0 <main>:
   100e0:	fe010113          	add	sp,sp,-32
   100e4:	00112e23          	sw	ra,28(sp)
   100e8:	00812c23          	sw	s0,24(sp)
   100ec:	02010413          	add	s0,sp,32
   100f0:	00100793          	li	a5,1
   100f4:	fef42623          	sw	a5,-20(s0)
   100f8:	0540006f          	j	1014c <main+0x6c>
   100fc:	fe842703          	lw	a4,-24(s0)
   10100:	00300793          	li	a5,3
   10104:	02f70e63          	beq	a4,a5,10140 <main+0x60>
   10108:	fe842703          	lw	a4,-24(s0)
   1010c:	00300793          	li	a5,3
   10110:	02e7cc63          	blt	a5,a4,10148 <main+0x68>
   10114:	fe842703          	lw	a4,-24(s0)
   10118:	00100793          	li	a5,1
   1011c:	00f70a63          	beq	a4,a5,10130 <main+0x50>
   10120:	fe842703          	lw	a4,-24(s0)
   10124:	00200793          	li	a5,2
   10128:	00f70863          	beq	a4,a5,10138 <main+0x58>
   1012c:	01c0006f          	j	10148 <main+0x68>
   10130:	f65ff0ef          	jal	10094 <incrementCount>
   10134:	0180006f          	j	1014c <main+0x6c>
   10138:	f8dff0ef          	jal	100c4 <displayCount>
   1013c:	0100006f          	j	1014c <main+0x6c>
   10140:	fe042623          	sw	zero,-20(s0)
   10144:	0080006f          	j	1014c <main+0x6c>
   10148:	00000013          	nop
   1014c:	fec42783          	lw	a5,-20(s0)
   10150:	fa0796e3          	bnez	a5,100fc <main+0x1c>
   10154:	00000793          	li	a5,0
   10158:	00078513          	mv	a0,a5
   1015c:	01c12083          	lw	ra,28(sp)
   10160:	01812403          	lw	s0,24(sp)
   10164:	02010113          	add	sp,sp,32
   10168:	00008067          	ret
```
My assembly code contains instructions like add, lui, sw, and so on.
Number of different instructions: 13
List of unique instructions:
```
add
sw
lui
lw
nop
ret
li
beq
blt
jal
j
bnez
mv
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
