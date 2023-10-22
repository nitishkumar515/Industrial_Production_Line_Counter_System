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
int sensor_output_pin=0;
int reset_pin=0;
int count=0;
int main ()
{

 
while(1)
    {
        if(reset_pin == 1)
        {
            asm volatile(
            "and %0, x30, 0"
         );
        }
        else if (sensor_output_pin == 1)
        {
        asm volatile(
        "add %0, X30, 1"
        :"r="(output)
        );
    }
   
}
return 0;
}



```

## Assembly code conversion

Compile the c program using RISCV-V GNU Toolchain and dump the assembly code into water_level_assembly.txt using the below commands.
```
riscv64-unknown-elf-gcc -march=rv32i -mabi=ilp32 -ffreestanding -nostdlib -o ./out plcount.c
riscv64-unknown-elf-objdump -d  -r out > pl_count_assembly.txt

```
```
out:     file format elf32-littleriscv


Disassembly of section .text:

00010074 <main>:
   10074:	ff010113          	addi	sp,sp,-16
   10078:	00812623          	sw	s0,12(sp)
   1007c:	01010413          	addi	s0,sp,16
   10080:	000117b7          	lui	a5,0x11
   10084:	0bc7a703          	lw	a4,188(a5) # 110bc <reset_pin>
   10088:	00100793          	li	a5,1
   1008c:	00f71663          	bne	a4,a5,10098 <main+0x24>
   10090:	8001a423          	sw	zero,-2040(gp) # 110c0 <count>
   10094:	fedff06f          	j	10080 <main+0xc>
   10098:	000117b7          	lui	a5,0x11
   1009c:	0b87a703          	lw	a4,184(a5) # 110b8 <__DATA_BEGIN__>
   100a0:	00100793          	li	a5,1
   100a4:	fcf71ee3          	bne	a4,a5,10080 <main+0xc>
   100a8:	8081a783          	lw	a5,-2040(gp) # 110c0 <count>
   100ac:	00178713          	addi	a4,a5,1
   100b0:	80e1a423          	sw	a4,-2040(gp) # 110c0 <count>
   100b4:	fcdff06f          	j	10080 <main+0xc>

```
Number of different instructions: 7
List of unique instructions:
```
addi
j
lui
sw
li
bne
lw

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
