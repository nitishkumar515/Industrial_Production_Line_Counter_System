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



## Block
![Screenshot from 2023-10-26 18-56-22](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/57b4e1cd-bac8-48b1-80c7-b67ebe9d1978)



## testing
* Design a function that executes the intended logic you require.
* Compile the code using the GCC compiler and verify the output:
```
gcc p_l_count.c
./a.out
```
case-1

reset-pin =0    sensor-output_pin =1

![Screenshot from 2023-11-03 12-30-13](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/189069a6-4087-49c9-8fe9-5f5fa67445eb)


case-2
reset-pin =1   sensor-output_pin =0

![Screenshot from 2023-11-03 12-29-46](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/f46ed169-6fae-4c92-8d3c-a2fc074e5147)



## In line assembly C code
```
void display(int number) {
printf("display count = %d\n",number);
}
 int main ()
{
    int reset_pin;            // Declared locally
    int sensor_output_pin;    // Declared locally
    int output=0; 
                      
    while(1)
    {
   
        if(reset_pin == 1)
        {
        int output=0;
            asm volatile(
            "and x30, x30, %0"
            : "=r" (output)    // Assuming you want to store the result in 'output'
            );
        }
        else if (sensor_output_pin == 1)
        {
        output = output +1;
            asm volatile(
            "add x30, x30, %0"
            : "=r" (output)   // Assuming you want to store the result in 'output'
            );
            
            
        }

         printf("output = %d\n",output);
         display(count);
        
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

00010054 <display>:
   10054:	fe010113          	addi	sp,sp,-32
   10058:	00812e23          	sw	s0,28(sp)
   1005c:	02010413          	addi	s0,sp,32
   10060:	fea42623          	sw	a0,-20(s0)
   10064:	00000013          	nop
   10068:	01c12403          	lw	s0,28(sp)
   1006c:	02010113          	addi	sp,sp,32
   10070:	00008067          	ret

00010074 <main>:
   10074:	fd010113          	addi	sp,sp,-48
   10078:	02112623          	sw	ra,44(sp)
   1007c:	02812423          	sw	s0,40(sp)
   10080:	03010413          	addi	s0,sp,48
   10084:	fe042623          	sw	zero,-20(s0)
   10088:	fe042223          	sw	zero,-28(s0)
   1008c:	00100793          	li	a5,1
   10090:	fef42023          	sw	a5,-32(s0)
   10094:	fe042423          	sw	zero,-24(s0)
   10098:	0540006f          	j	100ec <main+0x78>
   1009c:	fe442703          	lw	a4,-28(s0)
   100a0:	00100793          	li	a5,1
   100a4:	00f71a63          	bne	a4,a5,100b8 <main+0x44>
   100a8:	fc042e23          	sw	zero,-36(s0)
   100ac:	00ff7f33          	and	t5,t5,a5
   100b0:	fcf42e23          	sw	a5,-36(s0)
   100b4:	0240006f          	j	100d8 <main+0x64>
   100b8:	fe042703          	lw	a4,-32(s0)
   100bc:	00100793          	li	a5,1
   100c0:	00f71c63          	bne	a4,a5,100d8 <main+0x64>
   100c4:	fec42783          	lw	a5,-20(s0)
   100c8:	00178793          	addi	a5,a5,1
   100cc:	fef42623          	sw	a5,-20(s0)
   100d0:	00ff0f33          	add	t5,t5,a5
   100d4:	fef42623          	sw	a5,-20(s0)
   100d8:	fec42503          	lw	a0,-20(s0)
   100dc:	f79ff0ef          	jal	ra,10054 <display>
   100e0:	fe842783          	lw	a5,-24(s0)
   100e4:	00178793          	addi	a5,a5,1
   100e8:	fef42423          	sw	a5,-24(s0)
   100ec:	fe842703          	lw	a4,-24(s0)
   100f0:	00400793          	li	a5,4
   100f4:	fae7d4e3          	bge	a5,a4,1009c <main+0x28>
   100f8:	00000793          	li	a5,0
   100fc:	00078513          	mv	a0,a5
   10100:	02c12083          	lw	ra,44(sp)
   10104:	02812403          	lw	s0,40(sp)
   10108:	03010113          	addi	sp,sp,48
   1010c:	00008067          	ret

```
```
Number of different instructions: 13
List of unique instructions:
```
```
mv
addi
and
jal
lw
sw
j
bge
add
bne
nop
li
ret

```

## Spike results
instruction for spike results
```
riscv64-unknown-elf-gcc -march=rv64i -mabi=lp64 -ffreestanding -o out pl_counter.c
spike pk out
```
```
#include<stdio.h>
#include<stdlib.h>
void display(int number) {
printf("display count = %d\n",number);
}
 int main ()
{
    int reset_pin = 0;            // Declared locally
    int sensor_output_pin = 1;    // Declared locally
    int output=0; 
    int i =0;                  // Declared locally without initialization

    while(i<5)
    {
    i = i +1;
        if(reset_pin == 1)
        {
        int output=0;
            asm volatile(
            "and x30, x30, %0"
            : "=r" (output)    // Assuming you want to store the result in 'output'
            );
        }
        else if (sensor_output_pin == 1)
        {
        output = output +1;
            asm volatile(
            "add x30, x30, %0"
            : "=r" (output)   // Assuming you want to store the result in 'output'
            );
            
            
        } 
        
    }

display(count);
    return 0;
}
```
## output
### case-1
reset_pin ==0   sensor_outpin_pin ==1

[since , I have given loop max value = 5 so my output is upto 4, outherwise it can go up max limit of processor ]

![Screenshot from 2023-11-03 12-34-27](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/25b3e402-8e27-42e9-9d5f-bd6a268b4b4a)


### case-2
reset-pin ==1   sensor_output_pin ==0

![Screenshot from 2023-11-03 12-34-58](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/25b92f96-c941-4b4e-8544-b4ab768ba0fb)









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
