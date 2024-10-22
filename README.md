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


Here I am using, Infrared Obstacle Avoidance IR Sensor Module (Active Low) has a pair of infrared transmitting and receiving tubes. When the transmitted light waves are reflected back, the reflected IR waves will be received by the receiver tube. The onboard comparator circuitry does the processing and the green indicator LED comes to life.

### Sensor

![Screenshot from 2024-10-20 22-08-32](https://github.com/user-attachments/assets/d1454616-e256-4a32-99f3-464a0766de83)




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
void display(int num1, int num2);

 int main ()
{
    int reset_pin = 0;    
    int sensor_output_pin =1; 
    int output1=0;
    int output2=0;
    while(1)
    { 
    
        if(reset_pin == 1)
        {
              int output1=0;
              int output2=0;
         
        }
        else if (sensor_output_pin == 1)
        {
            if(output2==9 && output1==9)
             {
              output1=0;
              output2=0;
             }
            else if(output1==9)
               {
                 output2++;
                 output1=0;
               } 
                else
                {
                output1++;
                }
             
            }
            display(output1,output2); 
           
        }
       
     return 0;
}
    
voiid display(int num1, int num2)
{  
printf("display count = %d%d ",num2,num1);
int send,mask;
 switch(num1)
{
case 0:  send = 0xFFFF01FF; mask= 0xFFFFFF00;

              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)  
              );
              break;
case 1:  send = 0xFFFF4FFF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 2:  send = 0xFFFF12FF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 3:  send = 0xFFFF03FF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 4:  send = 0xFFFF4CFF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 5:  send = 0xFFFF24FF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 6:  send = 0xFFFF20FF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 7:  send = 0xFFFF0FFF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 8:  send = 0xFFFF00FF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 9:  send = 0xFFFF04FF; mask= 0xFFFFFF00;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
}

switch(num2)
{
case 0:  send = 0xFF01FFFF;  mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 1:  send = 0xFF4FFFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 2:  send = 0xFF12FFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 3:  send = 0xFF03FFFF;mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 4:  send = 0xFF4CFFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 5:  send = 0xFF24FFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 6:  send = 0xFF20FFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 7:  send = 0xFF0FFFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 8:  send = 0xFF00FFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;
case 9:  send = 0xFF04FFFF; mask= 0xFFFF00FF;
              asm volatile(
              "and x30, x30, %1\n\t"
              "and x30, x30, %0\n\t"
              : "=r" (send), "=r" (mask)
              );
              break;  
}
}


```


## Assembly code conversion

Compile the c program using RISCV-V GNU Toolchain and dump the assembly code into pl_counter_assembly.txt using the below commands.
```
riscv64-unknown-elf-gcc -march=rv32i -mabi=ilp32 -ffreestanding -nostdlib -o ./out pl_counter.c
riscv64-unknown-elf-objdump -d  -r out > pl_counter_assembly.txt

```
```

out:     file format elf32-littleriscv


Disassembly of section .text:

00010054 <main>:
   10054:	fd010113          	addi	sp,sp,-48
   10058:	02112623          	sw	ra,44(sp)
   1005c:	02812423          	sw	s0,40(sp)
   10060:	03010413          	addi	s0,sp,48
   10064:	fe042223          	sw	zero,-28(s0)
   10068:	fe042023          	sw	zero,-32(s0)
   1006c:	fe042623          	sw	zero,-20(s0)
   10070:	fe042423          	sw	zero,-24(s0)
   10074:	fe442703          	lw	a4,-28(s0)
   10078:	00100793          	li	a5,1
   1007c:	00f71863          	bne	a4,a5,1008c <main+0x38>
   10080:	fc042e23          	sw	zero,-36(s0)
   10084:	fc042c23          	sw	zero,-40(s0)
   10088:	0600006f          	j	100e8 <main+0x94>
   1008c:	fe042703          	lw	a4,-32(s0)
   10090:	00100793          	li	a5,1
   10094:	04f71a63          	bne	a4,a5,100e8 <main+0x94>
   10098:	fe842703          	lw	a4,-24(s0)
   1009c:	00900793          	li	a5,9
   100a0:	00f71e63          	bne	a4,a5,100bc <main+0x68>
   100a4:	fec42703          	lw	a4,-20(s0)
   100a8:	00900793          	li	a5,9
   100ac:	00f71863          	bne	a4,a5,100bc <main+0x68>
   100b0:	fe042623          	sw	zero,-20(s0)
   100b4:	fe042423          	sw	zero,-24(s0)
   100b8:	0300006f          	j	100e8 <main+0x94>
   100bc:	fec42703          	lw	a4,-20(s0)
   100c0:	00900793          	li	a5,9
   100c4:	00f71c63          	bne	a4,a5,100dc <main+0x88>
   100c8:	fe842783          	lw	a5,-24(s0)
   100cc:	00178793          	addi	a5,a5,1
   100d0:	fef42423          	sw	a5,-24(s0)
   100d4:	fe042623          	sw	zero,-20(s0)
   100d8:	0100006f          	j	100e8 <main+0x94>
   100dc:	fec42783          	lw	a5,-20(s0)
   100e0:	00178793          	addi	a5,a5,1
   100e4:	fef42623          	sw	a5,-20(s0)
   100e8:	fe842583          	lw	a1,-24(s0)
   100ec:	fec42503          	lw	a0,-20(s0)
   100f0:	008000ef          	jal	ra,100f8 <display>
   100f4:	f81ff06f          	j	10074 <main+0x20>

000100f8 <display>:
   100f8:	fd010113          	addi	sp,sp,-48
   100fc:	02812623          	sw	s0,44(sp)
   10100:	03010413          	addi	s0,sp,48
   10104:	fca42e23          	sw	a0,-36(s0)
   10108:	fcb42c23          	sw	a1,-40(s0)
   1010c:	fdc42703          	lw	a4,-36(s0)
   10110:	00900793          	li	a5,9
   10114:	1ae7e863          	bltu	a5,a4,102c4 <display+0x1cc>
   10118:	fdc42783          	lw	a5,-36(s0)
   1011c:	00279713          	slli	a4,a5,0x2
   10120:	000107b7          	lui	a5,0x10
   10124:	4b478793          	addi	a5,a5,1204 # 104b4 <display+0x3bc>
   10128:	00f707b3          	add	a5,a4,a5
   1012c:	0007a783          	lw	a5,0(a5)
   10130:	00078067          	jr	a5
   10134:	ffff07b7          	lui	a5,0xffff0
   10138:	1ff78793          	addi	a5,a5,511 # ffff01ff <__global_pointer$+0xfffde4fb>
   1013c:	fef42623          	sw	a5,-20(s0)
   10140:	f0000793          	li	a5,-256
   10144:	fef42423          	sw	a5,-24(s0)
   10148:	00ff7f33          	and	t5,t5,a5
   1014c:	00ef7f33          	and	t5,t5,a4
   10150:	fee42623          	sw	a4,-20(s0)
   10154:	fef42423          	sw	a5,-24(s0)
   10158:	16c0006f          	j	102c4 <display+0x1cc>
   1015c:	ffff57b7          	lui	a5,0xffff5
   10160:	fff78793          	addi	a5,a5,-1 # ffff4fff <__global_pointer$+0xfffe32fb>
   10164:	fef42623          	sw	a5,-20(s0)
   10168:	f0000793          	li	a5,-256
   1016c:	fef42423          	sw	a5,-24(s0)
   10170:	00ff7f33          	and	t5,t5,a5
   10174:	00ef7f33          	and	t5,t5,a4
   10178:	fee42623          	sw	a4,-20(s0)
   1017c:	fef42423          	sw	a5,-24(s0)
   10180:	1440006f          	j	102c4 <display+0x1cc>
   10184:	ffff17b7          	lui	a5,0xffff1
   10188:	2ff78793          	addi	a5,a5,767 # ffff12ff <__global_pointer$+0xfffdf5fb>
   1018c:	fef42623          	sw	a5,-20(s0)
   10190:	f0000793          	li	a5,-256
   10194:	fef42423          	sw	a5,-24(s0)
   10198:	00ff7f33          	and	t5,t5,a5
   1019c:	00ef7f33          	and	t5,t5,a4
   101a0:	fee42623          	sw	a4,-20(s0)
   101a4:	fef42423          	sw	a5,-24(s0)
   101a8:	11c0006f          	j	102c4 <display+0x1cc>
   101ac:	ffff07b7          	lui	a5,0xffff0
   101b0:	3ff78793          	addi	a5,a5,1023 # ffff03ff <__global_pointer$+0xfffde6fb>
   101b4:	fef42623          	sw	a5,-20(s0)
   101b8:	f0000793          	li	a5,-256
   101bc:	fef42423          	sw	a5,-24(s0)
   101c0:	00ff7f33          	and	t5,t5,a5
   101c4:	00ef7f33          	and	t5,t5,a4
   101c8:	fee42623          	sw	a4,-20(s0)
   101cc:	fef42423          	sw	a5,-24(s0)
   101d0:	0f40006f          	j	102c4 <display+0x1cc>
   101d4:	ffff57b7          	lui	a5,0xffff5
   101d8:	cff78793          	addi	a5,a5,-769 # ffff4cff <__global_pointer$+0xfffe2ffb>
   101dc:	fef42623          	sw	a5,-20(s0)
   101e0:	f0000793          	li	a5,-256
   101e4:	fef42423          	sw	a5,-24(s0)
   101e8:	00ff7f33          	and	t5,t5,a5
   101ec:	00ef7f33          	and	t5,t5,a4
   101f0:	fee42623          	sw	a4,-20(s0)
   101f4:	fef42423          	sw	a5,-24(s0)
   101f8:	0cc0006f          	j	102c4 <display+0x1cc>
   101fc:	ffff27b7          	lui	a5,0xffff2
   10200:	4ff78793          	addi	a5,a5,1279 # ffff24ff <__global_pointer$+0xfffe07fb>
   10204:	fef42623          	sw	a5,-20(s0)
   10208:	f0000793          	li	a5,-256
   1020c:	fef42423          	sw	a5,-24(s0)
   10210:	00ff7f33          	and	t5,t5,a5
   10214:	00ef7f33          	and	t5,t5,a4
   10218:	fee42623          	sw	a4,-20(s0)
   1021c:	fef42423          	sw	a5,-24(s0)
   10220:	0a40006f          	j	102c4 <display+0x1cc>
   10224:	ffff27b7          	lui	a5,0xffff2
   10228:	0ff78793          	addi	a5,a5,255 # ffff20ff <__global_pointer$+0xfffe03fb>
   1022c:	fef42623          	sw	a5,-20(s0)
   10230:	f0000793          	li	a5,-256
   10234:	fef42423          	sw	a5,-24(s0)
   10238:	00ff7f33          	and	t5,t5,a5
   1023c:	00ef7f33          	and	t5,t5,a4
   10240:	fee42623          	sw	a4,-20(s0)
   10244:	fef42423          	sw	a5,-24(s0)
   10248:	07c0006f          	j	102c4 <display+0x1cc>
   1024c:	ffff17b7          	lui	a5,0xffff1
   10250:	fff78793          	addi	a5,a5,-1 # ffff0fff <__global_pointer$+0xfffdf2fb>
   10254:	fef42623          	sw	a5,-20(s0)
   10258:	f0000793          	li	a5,-256
   1025c:	fef42423          	sw	a5,-24(s0)
   10260:	00ff7f33          	and	t5,t5,a5
   10264:	00ef7f33          	and	t5,t5,a4
   10268:	fee42623          	sw	a4,-20(s0)
   1026c:	fef42423          	sw	a5,-24(s0)
   10270:	0540006f          	j	102c4 <display+0x1cc>
   10274:	ffff07b7          	lui	a5,0xffff0
   10278:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   1027c:	fef42623          	sw	a5,-20(s0)
   10280:	f0000793          	li	a5,-256
   10284:	fef42423          	sw	a5,-24(s0)
   10288:	00ff7f33          	and	t5,t5,a5
   1028c:	00ef7f33          	and	t5,t5,a4
   10290:	fee42623          	sw	a4,-20(s0)
   10294:	fef42423          	sw	a5,-24(s0)
   10298:	02c0006f          	j	102c4 <display+0x1cc>
   1029c:	ffff07b7          	lui	a5,0xffff0
   102a0:	4ff78793          	addi	a5,a5,1279 # ffff04ff <__global_pointer$+0xfffde7fb>
   102a4:	fef42623          	sw	a5,-20(s0)
   102a8:	f0000793          	li	a5,-256
   102ac:	fef42423          	sw	a5,-24(s0)
   102b0:	00ff7f33          	and	t5,t5,a5
   102b4:	00ef7f33          	and	t5,t5,a4
   102b8:	fee42623          	sw	a4,-20(s0)
   102bc:	fef42423          	sw	a5,-24(s0)
   102c0:	00000013          	nop
   102c4:	fd842703          	lw	a4,-40(s0)
   102c8:	00900793          	li	a5,9
   102cc:	1ce7ec63          	bltu	a5,a4,104a4 <display+0x3ac>
   102d0:	fd842783          	lw	a5,-40(s0)
   102d4:	00279713          	slli	a4,a5,0x2
   102d8:	000107b7          	lui	a5,0x10
   102dc:	4dc78793          	addi	a5,a5,1244 # 104dc <display+0x3e4>
   102e0:	00f707b3          	add	a5,a4,a5
   102e4:	0007a783          	lw	a5,0(a5)
   102e8:	00078067          	jr	a5
   102ec:	ff0207b7          	lui	a5,0xff020
   102f0:	fff78793          	addi	a5,a5,-1 # ff01ffff <__global_pointer$+0xff00e2fb>
   102f4:	fef42623          	sw	a5,-20(s0)
   102f8:	ffff07b7          	lui	a5,0xffff0
   102fc:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   10300:	fef42423          	sw	a5,-24(s0)
   10304:	00ff7f33          	and	t5,t5,a5
   10308:	00ef7f33          	and	t5,t5,a4
   1030c:	fee42623          	sw	a4,-20(s0)
   10310:	fef42423          	sw	a5,-24(s0)
   10314:	1900006f          	j	104a4 <display+0x3ac>
   10318:	ff5007b7          	lui	a5,0xff500
   1031c:	fff78793          	addi	a5,a5,-1 # ff4fffff <__global_pointer$+0xff4ee2fb>
   10320:	fef42623          	sw	a5,-20(s0)
   10324:	ffff07b7          	lui	a5,0xffff0
   10328:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   1032c:	fef42423          	sw	a5,-24(s0)
   10330:	00ff7f33          	and	t5,t5,a5
   10334:	00ef7f33          	and	t5,t5,a4
   10338:	fee42623          	sw	a4,-20(s0)
   1033c:	fef42423          	sw	a5,-24(s0)
   10340:	1640006f          	j	104a4 <display+0x3ac>
   10344:	ff1307b7          	lui	a5,0xff130
   10348:	fff78793          	addi	a5,a5,-1 # ff12ffff <__global_pointer$+0xff11e2fb>
   1034c:	fef42623          	sw	a5,-20(s0)
   10350:	ffff07b7          	lui	a5,0xffff0
   10354:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   10358:	fef42423          	sw	a5,-24(s0)
   1035c:	00ff7f33          	and	t5,t5,a5
   10360:	00ef7f33          	and	t5,t5,a4
   10364:	fee42623          	sw	a4,-20(s0)
   10368:	fef42423          	sw	a5,-24(s0)
   1036c:	1380006f          	j	104a4 <display+0x3ac>
   10370:	ff0407b7          	lui	a5,0xff040
   10374:	fff78793          	addi	a5,a5,-1 # ff03ffff <__global_pointer$+0xff02e2fb>
   10378:	fef42623          	sw	a5,-20(s0)
   1037c:	ffff07b7          	lui	a5,0xffff0
   10380:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   10384:	fef42423          	sw	a5,-24(s0)
   10388:	00ff7f33          	and	t5,t5,a5
   1038c:	00ef7f33          	and	t5,t5,a4
   10390:	fee42623          	sw	a4,-20(s0)
   10394:	fef42423          	sw	a5,-24(s0)
   10398:	10c0006f          	j	104a4 <display+0x3ac>
   1039c:	ff4d07b7          	lui	a5,0xff4d0
   103a0:	fff78793          	addi	a5,a5,-1 # ff4cffff <__global_pointer$+0xff4be2fb>
   103a4:	fef42623          	sw	a5,-20(s0)
   103a8:	ffff07b7          	lui	a5,0xffff0
   103ac:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   103b0:	fef42423          	sw	a5,-24(s0)
   103b4:	00ff7f33          	and	t5,t5,a5
   103b8:	00ef7f33          	and	t5,t5,a4
   103bc:	fee42623          	sw	a4,-20(s0)
   103c0:	fef42423          	sw	a5,-24(s0)
   103c4:	0e00006f          	j	104a4 <display+0x3ac>
   103c8:	ff2507b7          	lui	a5,0xff250
   103cc:	fff78793          	addi	a5,a5,-1 # ff24ffff <__global_pointer$+0xff23e2fb>
   103d0:	fef42623          	sw	a5,-20(s0)
   103d4:	ffff07b7          	lui	a5,0xffff0
   103d8:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   103dc:	fef42423          	sw	a5,-24(s0)
   103e0:	00ff7f33          	and	t5,t5,a5
   103e4:	00ef7f33          	and	t5,t5,a4
   103e8:	fee42623          	sw	a4,-20(s0)
   103ec:	fef42423          	sw	a5,-24(s0)
   103f0:	0b40006f          	j	104a4 <display+0x3ac>
   103f4:	ff2107b7          	lui	a5,0xff210
   103f8:	fff78793          	addi	a5,a5,-1 # ff20ffff <__global_pointer$+0xff1fe2fb>
   103fc:	fef42623          	sw	a5,-20(s0)
   10400:	ffff07b7          	lui	a5,0xffff0
   10404:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   10408:	fef42423          	sw	a5,-24(s0)
   1040c:	00ff7f33          	and	t5,t5,a5
   10410:	00ef7f33          	and	t5,t5,a4
   10414:	fee42623          	sw	a4,-20(s0)
   10418:	fef42423          	sw	a5,-24(s0)
   1041c:	0880006f          	j	104a4 <display+0x3ac>
   10420:	ff1007b7          	lui	a5,0xff100
   10424:	fff78793          	addi	a5,a5,-1 # ff0fffff <__global_pointer$+0xff0ee2fb>
   10428:	fef42623          	sw	a5,-20(s0)
   1042c:	ffff07b7          	lui	a5,0xffff0
   10430:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   10434:	fef42423          	sw	a5,-24(s0)
   10438:	00ff7f33          	and	t5,t5,a5
   1043c:	00ef7f33          	and	t5,t5,a4
   10440:	fee42623          	sw	a4,-20(s0)
   10444:	fef42423          	sw	a5,-24(s0)
   10448:	05c0006f          	j	104a4 <display+0x3ac>
   1044c:	ff0107b7          	lui	a5,0xff010
   10450:	fff78793          	addi	a5,a5,-1 # ff00ffff <__global_pointer$+0xfeffe2fb>
   10454:	fef42623          	sw	a5,-20(s0)
   10458:	ffff07b7          	lui	a5,0xffff0
   1045c:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   10460:	fef42423          	sw	a5,-24(s0)
   10464:	00ff7f33          	and	t5,t5,a5
   10468:	00ef7f33          	and	t5,t5,a4
   1046c:	fee42623          	sw	a4,-20(s0)
   10470:	fef42423          	sw	a5,-24(s0)
   10474:	0300006f          	j	104a4 <display+0x3ac>
   10478:	ff0507b7          	lui	a5,0xff050
   1047c:	fff78793          	addi	a5,a5,-1 # ff04ffff <__global_pointer$+0xff03e2fb>
   10480:	fef42623          	sw	a5,-20(s0)
   10484:	ffff07b7          	lui	a5,0xffff0
   10488:	0ff78793          	addi	a5,a5,255 # ffff00ff <__global_pointer$+0xfffde3fb>
   1048c:	fef42423          	sw	a5,-24(s0)
   10490:	00ff7f33          	and	t5,t5,a5
   10494:	00ef7f33          	and	t5,t5,a4
   10498:	fee42623          	sw	a4,-20(s0)
   1049c:	fef42423          	sw	a5,-24(s0)
   104a0:	00000013          	nop
   104a4:	00000013          	nop
   104a8:	02c12403          	lw	s0,44(sp)
   104ac:	03010113          	addi	sp,sp,48
   104b0:	00008067          	ret



```
```
Number of different instructions: 15
List of unique instructions:
```
```
add
j
addi
sw
jal
slli
bltu
li
and
jr
lw
bne
ret
lui
nop

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
![Screenshot from 2023-11-10 18-27-04](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/44ef7016-e161-44b7-9f06-ea732a9cff43)

![Screenshot from 2023-11-10 18-27-34](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/a5822684-50fd-4e50-bad2-2fb9199d0dd2)


Folllowing are the commands to run the GLS simulation:
```
iverilog -o test synth_processor_test.v testbench.v sky130_sram_1kbyte_1rw1r_32x256_8.v sky130_fd_sc_hd.v primitives.v
./test
```
![Screenshot from 2023-11-10 20-39-18](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/b14aa904-e910-4763-8467-adc0841d6f8b)

![Screenshot from 2023-11-10 18-29-14](https://github.com/nitishkumar515/Industrial_Production_Line_Counter_System/assets/140998638/099613e2-ee93-4838-b94f-28e25900dd25)













## Word of Thanks
I sciencerly thank **Mr. Kunal Gosh(Founder/VSD)**

I sciencerly thank **Mr.Mayank Kabra,Founder,Chipcron Pvt.Ltd.**

## Acknowledgement

- Skywater Foundry
- Bhargav DV,MS
- alwin Shaju IIITB
  
## Reference 

- https://github.com/alwinshaju08/
- https://github.com/The-OpenROAD-Project/OpenSTA.git
- https://github.com/kunalg123
- https://www.vsdiat.com
- https://github.com/SakethGajawada/RISCV-GNU
- https://github.com/kunalg123
