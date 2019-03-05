---
layout: post
title: ARM汇编
---

ARM寄存器

```
R0: 
R1:  
R2: 
R3: 
R4:
R5:
R6:
R7:
R8:
R9:
R10:
R11:
R12:
R13:
R14: LR (Link Register).               自动保存函数的返回地址。
R15: PC (Program Counter).
CPSR:  Current Program Status Register    
  N:
  Z:
  C:(Carry)
  V:
 
  
```



ARM指令

```
ADRL: Load a program-relative or register-relative address into a register
B:    Branch
BX:   Branch and Exchange      跳转并切换(ARM或Thumb)状态
BCC:  Branch if Carry Clear    CPSR寄存器条件标志位为0时跳转
CMP:  Compare
CBZ:  Compare and Branch on Zero
CBNZ: Compare and Branch on Non-Zero
LDR:  Load
ADD:  Addition
SUB:  Subtraction
MOV:  Move data
PUSH: Push on Stack
POP:  Pop off Stack
```
