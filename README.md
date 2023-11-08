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
#include<stdio.h>
void display(int num);

 int main ()
{
    int reset_pin ;   
    int sensor_output_pin;    
    int output=0; 
   

    while(1)
    {

        if(reset_pin == 1)
        {
              int output=0;
              int temp = 0xFFFFFF00;
              int dn =   0xFF0101FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %2\n\t"
              : "=r" (output), "=r" (temp), "=r"(dn)   // Assuming you want to store the result in 'x30 register'
              );
        
        }
        else if (sensor_output_pin == 1)
        {
            if(output == 99)
             {
              output = 0;
              int temp = 0xFFFFFF00;
              int dn = 0xFF0101FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %2\n\t"
              : "=r" (output), "=r" (temp), "=r"(dn)   // Assuming you want to store the result in 'x30 register'
              );
              }
              else
               {
                 output = output +1;
          
                 asm volatile(
                 "add x30, x30, %0"
                 : "=r" (output)   // Assuming you want to store the result in 'x30 register'
                 ); 
            }
            
        }

        display(output);
    }
    return 0;
}


void display(int num)
{
 int first_digit, second_digit, send;
 
 
 
 first_digit = num%10;
 second_digit = num /10;
 switch(first_digit)
{
case 0:   send = 0xFFFF01FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 1:  send = 0xFFFF4FFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 2:  send = 0xFFFF12FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 3:  send = 0xFFFF03FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 4:  send = 0xFFFF4CFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 5:  send = 0xFFFF24FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 6:  send = 0xFFFF20FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 7:  send = 0xFFFF0FFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 8:  send = 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 9:  send = 0xFFFF04FF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
}
switch(second_digit)
{
case 0:  send = 0xFF01FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 1:  send = 0xFF4FFFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 2:  send = 0xFF12FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 3:  send = 0xFF03FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 4:  send = 0xFF4CFFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 5:  send = 0xFF24FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 6:  send = 0xFF20FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 7:  send = 0xFF0FFFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 8:  send = 0xFF00FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;
case 9:  send = 0xFF04FFFF;
              asm volatile(
              "and x30, x30, %0\n\t"
              : "=r" (send)   // Assuming you want to store the result in 'x30 register'
              );
              break;   
}

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
   10054:	fc010113          	addi	sp,sp,-64
   10058:	02112e23          	sw	ra,60(sp)
   1005c:	02812c23          	sw	s0,56(sp)
   10060:	04010413          	addi	s0,sp,64
   10064:	fe042223          	sw	zero,-28(s0)
   10068:	00100793          	li	a5,1
   1006c:	fef42023          	sw	a5,-32(s0)
   10070:	fe042623          	sw	zero,-20(s0)
   10074:	fe042423          	sw	zero,-24(s0)
   10078:	0b00006f          	j	10128 <main+0xd4>
   1007c:	fe842783          	lw	a5,-24(s0)
   10080:	00178793          	addi	a5,a5,1
   10084:	fef42423          	sw	a5,-24(s0)
   10088:	fe442703          	lw	a4,-28(s0)
   1008c:	00100793          	li	a5,1
   10090:	02f71a63          	bne	a4,a5,100c4 <main+0x70>
   10094:	fc042e23          	sw	zero,-36(s0)
   10098:	f0000793          	li	a5,-256
   1009c:	fcf42c23          	sw	a5,-40(s0)
   100a0:	ff0107b7          	lui	a5,0xff010
   100a4:	1ff78793          	addi	a5,a5,511 # ff0101ff <__global_pointer$+0xfeffe893>
   100a8:	fcf42a23          	sw	a5,-44(s0)
   100ac:	00ef7f33          	and	t5,t5,a4
   100b0:	00ff7f33          	and	t5,t5,a5
   100b4:	fcd42e23          	sw	a3,-36(s0)
   100b8:	fce42c23          	sw	a4,-40(s0)
   100bc:	fcf42a23          	sw	a5,-44(s0)
   100c0:	0600006f          	j	10120 <main+0xcc>
   100c4:	fe042703          	lw	a4,-32(s0)
   100c8:	00100793          	li	a5,1
   100cc:	04f71a63          	bne	a4,a5,10120 <main+0xcc>
   100d0:	fec42703          	lw	a4,-20(s0)
   100d4:	00300793          	li	a5,3
   100d8:	02f71a63          	bne	a4,a5,1010c <main+0xb8>
   100dc:	fe042623          	sw	zero,-20(s0)
   100e0:	f0000793          	li	a5,-256
   100e4:	fcf42823          	sw	a5,-48(s0)
   100e8:	ff0107b7          	lui	a5,0xff010
   100ec:	1ff78793          	addi	a5,a5,511 # ff0101ff <__global_pointer$+0xfeffe893>
   100f0:	fcf42623          	sw	a5,-52(s0)
   100f4:	00ef7f33          	and	t5,t5,a4
   100f8:	00ff7f33          	and	t5,t5,a5
   100fc:	fed42623          	sw	a3,-20(s0)
   10100:	fce42823          	sw	a4,-48(s0)
   10104:	fcf42623          	sw	a5,-52(s0)
   10108:	0180006f          	j	10120 <main+0xcc>
   1010c:	fec42783          	lw	a5,-20(s0)
   10110:	00178793          	addi	a5,a5,1
   10114:	fef42623          	sw	a5,-20(s0)
   10118:	00ff0f33          	add	t5,t5,a5
   1011c:	fef42623          	sw	a5,-20(s0)
   10120:	fec42503          	lw	a0,-20(s0)
   10124:	028000ef          	jal	ra,1014c <display>
   10128:	fe842703          	lw	a4,-24(s0)
   1012c:	00600793          	li	a5,6
   10130:	f4e7d6e3          	bge	a5,a4,1007c <main+0x28>
   10134:	00000793          	li	a5,0
   10138:	00078513          	mv	a0,a5
   1013c:	03c12083          	lw	ra,60(sp)
   10140:	03812403          	lw	s0,56(sp)
   10144:	04010113          	addi	sp,sp,64
   10148:	00008067          	ret

0001014c <display>:
   1014c:	fe010113          	addi	sp,sp,-32
   10150:	00812e23          	sw	s0,28(sp)
   10154:	02010413          	addi	s0,sp,32
   10158:	fea42623          	sw	a0,-20(s0)
   1015c:	00000013          	nop
   10160:	01c12403          	lw	s0,28(sp)
   10164:	02010113          	addi	sp,sp,32
   10168:	00008067          	ret

```
```
Number of different instructions: 14
List of unique instructions:
```
```
ret
nop
jal
sw
lui
and
bge
bne
li
addi
mv
add
lw
j


```

## Spike results


### output
instruction for spike result
```
riscv64-unknown-elf-gcc -march=rv64i -mabi=lp64 -ffreestanding -o out pl_counter.c
spike pk out
```
### case-1
reset_pin ==0   sensor_outpin_pin ==1

[since , I have given loop max value = 5 so my output is upto 5, outherwise it can go up max limit of processor ]

![Screenshot from 2023-11-03 12-34-27](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/25b3e402-8e27-42e9-9d5f-bd6a268b4b4a)


### case-2
reset-pin ==1   sensor_output_pin ==0

![Screenshot from 2023-11-03 12-34-58](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/25b92f96-c941-4b4e-8544-b4ab768ba0fb)

## Functional Simulation In GTKWave :
![Screenshot from 2023-11-03 15-26-03](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/a9e5393b-3011-4fd7-b0ef-258a10bd2ede)

## Synthesis :

Synthesis is the process of converting RTL code into a gate-level netlist. It involves mapping the functionality specified in the RTL code to a library of standard cells, such as NAND, NOR, XOR gates, etc., provided by the target technology.
Synthesis takes place in multiple steps :
* Converting RTL into simple logic gates.
* Mapping those gates to actual technology-dependent logic gates available in the technology libraries.
* Optimizing the mapped netlist keeping the constraints set by the designer intact.
## Gate Level Simulation :
Gate level Simulation(GLS) is done at the late level of Design cycle. This is run after the RTL code is synthesized into Netlist. Netlist is translation from RTL into Gates and connection wirings with full functional and timing behaviour. Netlist is logically same as RTL code, therefore, same test bench can be used for it.We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met. Folllowing are the commands to we need to convert Rtl code to netlist in yosys for that commands are :
```
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80_256.lib 
read_verilog processor.v 
synth -top wrapper
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80_256.lib 
abc -liberty sky130_fd_sc_hd__tt_025C_1v80_256.lib
write_verilog synth_processor_test.v
show wrapper

```
![Screenshot from 2023-11-03 18-36-10](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/62ac1c60-3c11-491b-a973-cb24e11e114e)
![Screenshot from 2023-11-03 18-37-09](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/7bfa95d8-328e-4f7e-a89f-dbe43ad8dbc5)

Folllowing are the commands to run the GLS simulation:
```
iverilog -o test synth_processor_test.v testbench.v sky130_sram_1kbyte_1rw1r_32x256_8.v sky130_fd_sc_hd.v primitives.v
./test
```
![Screenshot from 2023-11-03 18-27-39](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/d49ec654-540e-4339-9032-2a38257f930b)

![Screenshot from 2023-11-08 10-57-14](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/bfcfe103-4104-4ef2-81fb-5125da22188f)













## Word of Thanks
I sciencerly thank **Mr. Kunal Gosh**(Founder/**VSD**)

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
