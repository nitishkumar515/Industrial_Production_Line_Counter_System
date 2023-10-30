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

reset-pin =0
sensor-output_pin =1

![Screenshot from 2023-10-30 10-30-38](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/7c82585d-e9fd-4745-bfdc-17ebbf23fe28)

case-2
reset-pin =1
sensor-output_pin =0

![Screenshot from 2023-10-30 10-29-43](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/7efc5c86-8565-49e7-addf-cd4fe38d7bb5)


## In line assembly C code
```
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
   10064:	fe842703          	lw	a4,-24(s0)
   10068:	00100793          	li	a5,1
   1006c:	00f71a63          	bne	a4,a5,10080 <main+0x2c>
   10070:	fe042223          	sw	zero,-28(s0)
   10074:	00ff7f33          	and	t5,t5,a5
   10078:	fef42223          	sw	a5,-28(s0)
   1007c:	fe9ff06f          	j	10064 <main+0x10>
   10080:	fe042703          	lw	a4,-32(s0)
   10084:	00100793          	li	a5,1
   10088:	fcf71ee3          	bne	a4,a5,10064 <main+0x10>
   1008c:	fec42783          	lw	a5,-20(s0)
   10090:	00178793          	addi	a5,a5,1
   10094:	fef42623          	sw	a5,-20(s0)
   10098:	00ff0f33          	add	t5,t5,a5
   1009c:	fef42623          	sw	a5,-20(s0)
   100a0:	fc5ff06f          	j	10064 <main+0x10>
```
```
Number of different instructions: 8
List of unique instructions:
```
```

add
li
sw
addi
and
bne
j
lw


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
printf("sum= %d\n",output);
    return 0;
}
```
## output
### case-1
reset_pin ==0
sensor_outpin_pin ==1

[since , I have given loop max value = 5 so my output is upto 4, outherwise it can go up max limit of processor ]

![Screenshot from 2023-10-30 20-56-18](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/129cc4b5-326c-4c7d-a575-d280ca4b80ef)

### case-2
reset-pin ==1
sensor_output_pin ==0

![Screenshot from 2023-10-30 20-56-46](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/a1ff80fc-aef1-4799-9204-36771cde76be)








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
