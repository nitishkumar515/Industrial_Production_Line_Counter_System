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
int main ()
{
    int reset_pin = 0;            // Declared locally
    int sensor_output_pin = 0;    // Declared locally
    int output;                   // Declared locally without initialization

    while(1)
    {
        if(reset_pin == 1)
        {
            asm volatile(
            "and %0, x30, 0"
            : "=r" (output)    // Assuming you want to store the result in 'output'
            );
        }
        else if (sensor_output_pin == 1)
        {
            asm volatile(
            "add %0, X30, 1"
            : "=r" (output)
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

00010054 <main>:
   10054:	fe010113          	addi	sp,sp,-32
   10058:	00812e23          	sw	s0,28(sp)
   1005c:	02010413          	addi	s0,sp,32
   10060:	fe042623          	sw	zero,-20(s0)
   10064:	fe042423          	sw	zero,-24(s0)
   10068:	fec42703          	lw	a4,-20(s0)
   1006c:	00100793          	li	a5,1
   10070:	00f71863          	bne	a4,a5,10080 <main+0x2c>
   10074:	000f7793          	andi	a5,t5,0
   10078:	fef42223          	sw	a5,-28(s0)
   1007c:	fedff06f          	j	10068 <main+0x14>
   10080:	fe842703          	lw	a4,-24(s0)
   10084:	00100793          	li	a5,1
   10088:	fef710e3          	bne	a4,a5,10068 <main+0x14>
   1008c:	001f0f13          	addi	t5,t5,1
   10090:	fef42223          	sw	a5,-28(s0)
   10094:	fd5ff06f          	j	10068 <main+0x14>
```
```
Number of different instructions: 7
List of unique instructions:
```
```
bne
li
lw
sw
andi
j
addi
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
