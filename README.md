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

ex.o:     file format elf64-littleriscv


Disassembly of section .text:

00000000000100b0 <main>:
   100b0:	f601a703          	lw	a4,-160(gp) # 11db8 <count>
   100b4:	00000793          	li	a5,0
   100b8:	00200593          	li	a1,2
   100bc:	00400613          	li	a2,4
   100c0:	00100693          	li	a3,1
   100c4:	00b78a63          	beq	a5,a1,100d8 <main+0x28>
   100c8:	00c78e63          	beq	a5,a2,100e4 <main+0x34>
   100cc:	fed79ce3          	bne	a5,a3,100c4 <main+0x14>
   100d0:	0017071b          	addw	a4,a4,1
   100d4:	feb79ae3          	bne	a5,a1,100c8 <main+0x18>
   100d8:	fee056e3          	blez	a4,100c4 <main+0x14>
   100dc:	fff7071b          	addw	a4,a4,-1
   100e0:	fe5ff06f          	j	100c4 <main+0x14>
   100e4:	f6e1a023          	sw	a4,-160(gp) # 11db8 <count>
   100e8:	00000513          	li	a0,0
   100ec:	00008067          	ret

00000000000100f0 <register_fini>:
   100f0:	ffff0797          	auipc	a5,0xffff0
   100f4:	f1078793          	add	a5,a5,-240 # 0 <main-0x100b0>
   100f8:	00078863          	beqz	a5,10108 <register_fini+0x18>
   100fc:	00000517          	auipc	a0,0x0
   10100:	15450513          	add	a0,a0,340 # 10250 <__libc_fini_array>
   10104:	1040006f          	j	10208 <atexit>
   10108:	00008067          	ret

000000000001010c <_start>:
   1010c:	00002197          	auipc	gp,0x2
   10110:	d4c18193          	add	gp,gp,-692 # 11e58 <__global_pointer$>
   10114:	f6018513          	add	a0,gp,-160 # 11db8 <count>
   10118:	fa018613          	add	a2,gp,-96 # 11df8 <__BSS_END__>
   1011c:	40a60633          	sub	a2,a2,a0
   10120:	00000593          	li	a1,0
   10124:	21c000ef          	jal	10340 <memset>
   10128:	00000517          	auipc	a0,0x0
   1012c:	12850513          	add	a0,a0,296 # 10250 <__libc_fini_array>
   10130:	0d8000ef          	jal	10208 <atexit>
   10134:	178000ef          	jal	102ac <__libc_init_array>
   10138:	00012503          	lw	a0,0(sp)
   1013c:	00810593          	add	a1,sp,8
   10140:	00000613          	li	a2,0
   10144:	f6dff0ef          	jal	100b0 <main>
   10148:	0d40006f          	j	1021c <exit>

000000000001014c <__do_global_dtors_aux>:
   1014c:	f681c783          	lbu	a5,-152(gp) # 11dc0 <completed.5468>
   10150:	04079463          	bnez	a5,10198 <__do_global_dtors_aux+0x4c>
   10154:	ffff0797          	auipc	a5,0xffff0
   10158:	eac78793          	add	a5,a5,-340 # 0 <main-0x100b0>
   1015c:	02078863          	beqz	a5,1018c <__do_global_dtors_aux+0x40>
   10160:	ff010113          	add	sp,sp,-16
   10164:	00001517          	auipc	a0,0x1
   10168:	4d850513          	add	a0,a0,1240 # 1163c <__FRAME_END__>
   1016c:	00113423          	sd	ra,8(sp)
   10170:	00000097          	auipc	ra,0x0
   10174:	000000e7          	jalr	zero # 0 <main-0x100b0>
   10178:	00813083          	ld	ra,8(sp)
   1017c:	00100793          	li	a5,1
   10180:	f6f18423          	sb	a5,-152(gp) # 11dc0 <completed.5468>
   10184:	01010113          	add	sp,sp,16
   10188:	00008067          	ret
   1018c:	00100793          	li	a5,1
   10190:	f6f18423          	sb	a5,-152(gp) # 11dc0 <completed.5468>
   10194:	00008067          	ret
   10198:	00008067          	ret

000000000001019c <frame_dummy>:
   1019c:	ffff0797          	auipc	a5,0xffff0
   101a0:	e6478793          	add	a5,a5,-412 # 0 <main-0x100b0>
   101a4:	00078c63          	beqz	a5,101bc <frame_dummy+0x20>
   101a8:	f7018593          	add	a1,gp,-144 # 11dc8 <object.5473>
   101ac:	00001517          	auipc	a0,0x1
   101b0:	49050513          	add	a0,a0,1168 # 1163c <__FRAME_END__>
   101b4:	00000317          	auipc	t1,0x0
   101b8:	00000067          	jr	zero # 0 <main-0x100b0>
   101bc:	00008067          	ret

00000000000101c0 <incrementCount>:
   101c0:	f601a783          	lw	a5,-160(gp) # 11db8 <count>
   101c4:	0017879b          	addw	a5,a5,1
   101c8:	f6f1a023          	sw	a5,-160(gp) # 11db8 <count>
   101cc:	00008067          	ret

00000000000101d0 <decrementCount>:
   101d0:	f601a783          	lw	a5,-160(gp) # 11db8 <count>
   101d4:	00f05663          	blez	a5,101e0 <decrementCount+0x10>
   101d8:	fff7879b          	addw	a5,a5,-1
   101dc:	f6f1a023          	sw	a5,-160(gp) # 11db8 <count>
   101e0:	00008067          	ret

00000000000101e4 <displayCount>:
   101e4:	00008067          	ret

00000000000101e8 <load>:
   101e8:	00050733          	add	a4,a0,zero
   101ec:	00b50633          	add	a2,a0,a1
   101f0:	000506b3          	add	a3,a0,zero

00000000000101f4 <loop>:
   101f4:	00e68733          	add	a4,a3,a4
   101f8:	00168693          	add	a3,a3,1
   101fc:	fec6cce3          	blt	a3,a2,101f4 <loop>
   10200:	00070533          	add	a0,a4,zero
   10204:	00008067          	ret

0000000000010208 <atexit>:
   10208:	00050593          	mv	a1,a0
   1020c:	00000693          	li	a3,0
   10210:	00000613          	li	a2,0
   10214:	00000513          	li	a0,0
   10218:	2040006f          	j	1041c <__register_exitproc>

000000000001021c <exit>:
   1021c:	ff010113          	add	sp,sp,-16
   10220:	00000593          	li	a1,0
   10224:	00813023          	sd	s0,0(sp)
   10228:	00113423          	sd	ra,8(sp)
   1022c:	00050413          	mv	s0,a0
   10230:	298000ef          	jal	104c8 <__call_exitprocs>
   10234:	f4818793          	add	a5,gp,-184 # 11da0 <_global_impure_ptr>
   10238:	0007b503          	ld	a0,0(a5)
   1023c:	05853783          	ld	a5,88(a0)
   10240:	00078463          	beqz	a5,10248 <exit+0x2c>
   10244:	000780e7          	jalr	a5
   10248:	00040513          	mv	a0,s0
   1024c:	3a0000ef          	jal	105ec <_exit>

0000000000010250 <__libc_fini_array>:
   10250:	fe010113          	add	sp,sp,-32
   10254:	00813823          	sd	s0,16(sp)
   10258:	00001797          	auipc	a5,0x1
   1025c:	40078793          	add	a5,a5,1024 # 11658 <impure_data>
   10260:	00001417          	auipc	s0,0x1
   10264:	3f040413          	add	s0,s0,1008 # 11650 <__do_global_dtors_aux_fini_array_entry>
   10268:	408787b3          	sub	a5,a5,s0
   1026c:	00913423          	sd	s1,8(sp)
   10270:	00113c23          	sd	ra,24(sp)
   10274:	4037d493          	sra	s1,a5,0x3
   10278:	02048063          	beqz	s1,10298 <__libc_fini_array+0x48>
   1027c:	ff878793          	add	a5,a5,-8
   10280:	00878433          	add	s0,a5,s0
   10284:	00043783          	ld	a5,0(s0)
   10288:	fff48493          	add	s1,s1,-1
   1028c:	ff840413          	add	s0,s0,-8
   10290:	000780e7          	jalr	a5
   10294:	fe0498e3          	bnez	s1,10284 <__libc_fini_array+0x34>
   10298:	01813083          	ld	ra,24(sp)
   1029c:	01013403          	ld	s0,16(sp)
   102a0:	00813483          	ld	s1,8(sp)
   102a4:	02010113          	add	sp,sp,32
   102a8:	00008067          	ret

00000000000102ac <__libc_init_array>:
   102ac:	fe010113          	add	sp,sp,-32
   102b0:	00813823          	sd	s0,16(sp)
   102b4:	01213023          	sd	s2,0(sp)
   102b8:	00001417          	auipc	s0,0x1
   102bc:	38840413          	add	s0,s0,904 # 11640 <__init_array_start>
   102c0:	00001917          	auipc	s2,0x1
   102c4:	38090913          	add	s2,s2,896 # 11640 <__init_array_start>
   102c8:	40890933          	sub	s2,s2,s0
   102cc:	00113c23          	sd	ra,24(sp)
   102d0:	00913423          	sd	s1,8(sp)
   102d4:	40395913          	sra	s2,s2,0x3
   102d8:	00090e63          	beqz	s2,102f4 <__libc_init_array+0x48>
   102dc:	00000493          	li	s1,0
   102e0:	00043783          	ld	a5,0(s0)
   102e4:	00148493          	add	s1,s1,1
   102e8:	00840413          	add	s0,s0,8
   102ec:	000780e7          	jalr	a5
   102f0:	fe9918e3          	bne	s2,s1,102e0 <__libc_init_array+0x34>
   102f4:	00001417          	auipc	s0,0x1
   102f8:	34c40413          	add	s0,s0,844 # 11640 <__init_array_start>
   102fc:	00001917          	auipc	s2,0x1
   10300:	35490913          	add	s2,s2,852 # 11650 <__do_global_dtors_aux_fini_array_entry>
   10304:	40890933          	sub	s2,s2,s0
   10308:	40395913          	sra	s2,s2,0x3
   1030c:	00090e63          	beqz	s2,10328 <__libc_init_array+0x7c>
   10310:	00000493          	li	s1,0
   10314:	00043783          	ld	a5,0(s0)
   10318:	00148493          	add	s1,s1,1
   1031c:	00840413          	add	s0,s0,8
   10320:	000780e7          	jalr	a5
   10324:	fe9918e3          	bne	s2,s1,10314 <__libc_init_array+0x68>
   10328:	01813083          	ld	ra,24(sp)
   1032c:	01013403          	ld	s0,16(sp)
   10330:	00813483          	ld	s1,8(sp)
   10334:	00013903          	ld	s2,0(sp)
   10338:	02010113          	add	sp,sp,32
   1033c:	00008067          	ret

0000000000010340 <memset>:
   10340:	00f00313          	li	t1,15
   10344:	00050713          	mv	a4,a0
   10348:	02c37a63          	bgeu	t1,a2,1037c <memset+0x3c>
   1034c:	00f77793          	and	a5,a4,15
   10350:	0a079063          	bnez	a5,103f0 <memset+0xb0>
   10354:	06059e63          	bnez	a1,103d0 <memset+0x90>
   10358:	ff067693          	and	a3,a2,-16
   1035c:	00f67613          	and	a2,a2,15
   10360:	00e686b3          	add	a3,a3,a4
   10364:	00b73023          	sd	a1,0(a4)
   10368:	00b73423          	sd	a1,8(a4)
   1036c:	01070713          	add	a4,a4,16
   10370:	fed76ae3          	bltu	a4,a3,10364 <memset+0x24>
   10374:	00061463          	bnez	a2,1037c <memset+0x3c>
   10378:	00008067          	ret
   1037c:	40c306b3          	sub	a3,t1,a2
   10380:	00269693          	sll	a3,a3,0x2
   10384:	00000297          	auipc	t0,0x0
   10388:	005686b3          	add	a3,a3,t0
   1038c:	00c68067          	jr	12(a3)
   10390:	00b70723          	sb	a1,14(a4)
   10394:	00b706a3          	sb	a1,13(a4)
   10398:	00b70623          	sb	a1,12(a4)
   1039c:	00b705a3          	sb	a1,11(a4)
   103a0:	00b70523          	sb	a1,10(a4)
   103a4:	00b704a3          	sb	a1,9(a4)
   103a8:	00b70423          	sb	a1,8(a4)
   103ac:	00b703a3          	sb	a1,7(a4)
   103b0:	00b70323          	sb	a1,6(a4)
   103b4:	00b702a3          	sb	a1,5(a4)
   103b8:	00b70223          	sb	a1,4(a4)
   103bc:	00b701a3          	sb	a1,3(a4)
   103c0:	00b70123          	sb	a1,2(a4)
   103c4:	00b700a3          	sb	a1,1(a4)
   103c8:	00b70023          	sb	a1,0(a4)
   103cc:	00008067          	ret
   103d0:	0ff5f593          	zext.b	a1,a1
   103d4:	00859693          	sll	a3,a1,0x8
   103d8:	00d5e5b3          	or	a1,a1,a3
   103dc:	01059693          	sll	a3,a1,0x10
   103e0:	00d5e5b3          	or	a1,a1,a3
   103e4:	02059693          	sll	a3,a1,0x20
   103e8:	00d5e5b3          	or	a1,a1,a3
   103ec:	f6dff06f          	j	10358 <memset+0x18>
   103f0:	00279693          	sll	a3,a5,0x2
   103f4:	00000297          	auipc	t0,0x0
   103f8:	005686b3          	add	a3,a3,t0
   103fc:	00008293          	mv	t0,ra
   10400:	f98680e7          	jalr	-104(a3)
   10404:	00028093          	mv	ra,t0
   10408:	ff078793          	add	a5,a5,-16
   1040c:	40f70733          	sub	a4,a4,a5
   10410:	00f60633          	add	a2,a2,a5
   10414:	f6c374e3          	bgeu	t1,a2,1037c <memset+0x3c>
   10418:	f3dff06f          	j	10354 <memset+0x14>

000000000001041c <__register_exitproc>:
   1041c:	f4818793          	add	a5,gp,-184 # 11da0 <_global_impure_ptr>
   10420:	0007b703          	ld	a4,0(a5)
   10424:	1f873783          	ld	a5,504(a4)
   10428:	06078063          	beqz	a5,10488 <__register_exitproc+0x6c>
   1042c:	0087a703          	lw	a4,8(a5)
   10430:	01f00813          	li	a6,31
   10434:	08e84663          	blt	a6,a4,104c0 <__register_exitproc+0xa4>
   10438:	02050863          	beqz	a0,10468 <__register_exitproc+0x4c>
   1043c:	00371813          	sll	a6,a4,0x3
   10440:	01078833          	add	a6,a5,a6
   10444:	10c83823          	sd	a2,272(a6)
   10448:	3107a883          	lw	a7,784(a5)
   1044c:	00100613          	li	a2,1
   10450:	00e6163b          	sllw	a2,a2,a4
   10454:	00c8e8b3          	or	a7,a7,a2
   10458:	3117a823          	sw	a7,784(a5)
   1045c:	20d83823          	sd	a3,528(a6)
   10460:	00200693          	li	a3,2
   10464:	02d50863          	beq	a0,a3,10494 <__register_exitproc+0x78>
   10468:	00270693          	add	a3,a4,2
   1046c:	00369693          	sll	a3,a3,0x3
   10470:	0017071b          	addw	a4,a4,1
   10474:	00e7a423          	sw	a4,8(a5)
   10478:	00d787b3          	add	a5,a5,a3
   1047c:	00b7b023          	sd	a1,0(a5)
   10480:	00000513          	li	a0,0
   10484:	00008067          	ret
   10488:	20070793          	add	a5,a4,512
   1048c:	1ef73c23          	sd	a5,504(a4)
   10490:	f9dff06f          	j	1042c <__register_exitproc+0x10>
   10494:	3147a683          	lw	a3,788(a5)
   10498:	00000513          	li	a0,0
   1049c:	00c6e633          	or	a2,a3,a2
   104a0:	00270693          	add	a3,a4,2
   104a4:	00369693          	sll	a3,a3,0x3
   104a8:	0017071b          	addw	a4,a4,1
   104ac:	30c7aa23          	sw	a2,788(a5)
   104b0:	00e7a423          	sw	a4,8(a5)
   104b4:	00d787b3          	add	a5,a5,a3
   104b8:	00b7b023          	sd	a1,0(a5)
   104bc:	00008067          	ret
   104c0:	fff00513          	li	a0,-1
   104c4:	00008067          	ret

00000000000104c8 <__call_exitprocs>:
   104c8:	fb010113          	add	sp,sp,-80
   104cc:	f4818793          	add	a5,gp,-184 # 11da0 <_global_impure_ptr>
   104d0:	01813023          	sd	s8,0(sp)
   104d4:	0007bc03          	ld	s8,0(a5)
   104d8:	03313423          	sd	s3,40(sp)
   104dc:	03413023          	sd	s4,32(sp)
   104e0:	01513c23          	sd	s5,24(sp)
   104e4:	01613823          	sd	s6,16(sp)
   104e8:	04113423          	sd	ra,72(sp)
   104ec:	04813023          	sd	s0,64(sp)
   104f0:	02913c23          	sd	s1,56(sp)
   104f4:	03213823          	sd	s2,48(sp)
   104f8:	01713423          	sd	s7,8(sp)
   104fc:	00050a93          	mv	s5,a0
   10500:	00058b13          	mv	s6,a1
   10504:	00100a13          	li	s4,1
   10508:	fff00993          	li	s3,-1
   1050c:	1f8c3903          	ld	s2,504(s8)
   10510:	02090863          	beqz	s2,10540 <__call_exitprocs+0x78>
   10514:	00892483          	lw	s1,8(s2)
   10518:	fff4841b          	addw	s0,s1,-1
   1051c:	02044263          	bltz	s0,10540 <__call_exitprocs+0x78>
   10520:	00349493          	sll	s1,s1,0x3
   10524:	009904b3          	add	s1,s2,s1
   10528:	040b0463          	beqz	s6,10570 <__call_exitprocs+0xa8>
   1052c:	2084b783          	ld	a5,520(s1)
   10530:	05678063          	beq	a5,s6,10570 <__call_exitprocs+0xa8>
   10534:	fff4041b          	addw	s0,s0,-1
   10538:	ff848493          	add	s1,s1,-8
   1053c:	ff3416e3          	bne	s0,s3,10528 <__call_exitprocs+0x60>
   10540:	04813083          	ld	ra,72(sp)
   10544:	04013403          	ld	s0,64(sp)
   10548:	03813483          	ld	s1,56(sp)
   1054c:	03013903          	ld	s2,48(sp)
   10550:	02813983          	ld	s3,40(sp)
   10554:	02013a03          	ld	s4,32(sp)
   10558:	01813a83          	ld	s5,24(sp)
   1055c:	01013b03          	ld	s6,16(sp)
   10560:	00813b83          	ld	s7,8(sp)
   10564:	00013c03          	ld	s8,0(sp)
   10568:	05010113          	add	sp,sp,80
   1056c:	00008067          	ret
   10570:	00892783          	lw	a5,8(s2)
   10574:	0084b703          	ld	a4,8(s1)
   10578:	fff7879b          	addw	a5,a5,-1
   1057c:	04878e63          	beq	a5,s0,105d8 <__call_exitprocs+0x110>
   10580:	0004b423          	sd	zero,8(s1)
   10584:	fa0708e3          	beqz	a4,10534 <__call_exitprocs+0x6c>
   10588:	31092783          	lw	a5,784(s2)
   1058c:	008a16bb          	sllw	a3,s4,s0
   10590:	00892b83          	lw	s7,8(s2)
   10594:	00d7f7b3          	and	a5,a5,a3
   10598:	0007879b          	sext.w	a5,a5
   1059c:	00079e63          	bnez	a5,105b8 <__call_exitprocs+0xf0>
   105a0:	000700e7          	jalr	a4
   105a4:	00892783          	lw	a5,8(s2)
   105a8:	f77792e3          	bne	a5,s7,1050c <__call_exitprocs+0x44>
   105ac:	1f8c3783          	ld	a5,504(s8)
   105b0:	f92782e3          	beq	a5,s2,10534 <__call_exitprocs+0x6c>
   105b4:	f59ff06f          	j	1050c <__call_exitprocs+0x44>
   105b8:	31492783          	lw	a5,788(s2)
   105bc:	1084b583          	ld	a1,264(s1)
   105c0:	00d7f7b3          	and	a5,a5,a3
   105c4:	0007879b          	sext.w	a5,a5
   105c8:	00079c63          	bnez	a5,105e0 <__call_exitprocs+0x118>
   105cc:	000a8513          	mv	a0,s5
   105d0:	000700e7          	jalr	a4
   105d4:	fd1ff06f          	j	105a4 <__call_exitprocs+0xdc>
   105d8:	00892423          	sw	s0,8(s2)
   105dc:	fa9ff06f          	j	10584 <__call_exitprocs+0xbc>
   105e0:	00058513          	mv	a0,a1
   105e4:	000700e7          	jalr	a4
   105e8:	fbdff06f          	j	105a4 <__call_exitprocs+0xdc>

00000000000105ec <_exit>:
   105ec:	00000593          	li	a1,0
   105f0:	00000613          	li	a2,0
   105f4:	00000693          	li	a3,0
   105f8:	00000713          	li	a4,0
   105fc:	00000793          	li	a5,0
   10600:	05d00893          	li	a7,93
   10604:	00000073          	ecall
   10608:	00054463          	bltz	a0,10610 <_exit+0x24>
   1060c:	0000006f          	j	1060c <_exit+0x20>
   10610:	ff010113          	add	sp,sp,-16
   10614:	00813023          	sd	s0,0(sp)
   10618:	00050413          	mv	s0,a0
   1061c:	00113423          	sd	ra,8(sp)
   10620:	4080043b          	negw	s0,s0
   10624:	00c000ef          	jal	10630 <__errno>
   10628:	00852023          	sw	s0,0(a0)
   1062c:	0000006f          	j	1062c <_exit+0x40>

0000000000010630 <__errno>:
   10630:	f5818793          	add	a5,gp,-168 # 11db0 <_impure_ptr>
   10634:	0007b503          	ld	a0,0(a5)
   10638:	00008067          	ret
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
