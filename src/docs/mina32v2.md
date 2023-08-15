The following section describes the **MINA32v2** base integer ISA.

# Overview

MINA32v2 has thirty-two 32-bit general-purpose registers (**R0**-**R31**).

Branch instructions target the special **IA** (Instruction Address) register, which holds the address of the current instruction.

The `BL` and `BLT` instructions save the return address in register **R31** (**LA**, Link Address).

# **Recommended register usage**

Name       | Alias  | Usage
:---------:|:------:|:---------------------------------
R0-R7      | A0-A7  | Function arguments/return values
R8-R15     | V0-V7  | Temporary (call-clobbered)
R16-R27    | S0-S12 | Temporary (call-preserved)
R28        | IP     | Intra-procedure call temporary
R29        | FP     | Frame pointer
R30        | SP     | Stack pointer
R31        | LA     | Return address (Link Address)

# **Instruction formats**

MINA32v2 defines four core instruction formats. Instructions are 32-bit wide and *must* be aligned on a 4-byte boundary; a misaligned **IA** will generate an exception.

```
3   22     21 11   11
1   76     09 76   21   76     0
BBBBBXXXXXXXXXXAAAAADDDDD0XXXXXX | R-type (Register)
iiiiiiiiiiiiXXXSSSSSDDDDD1XXXXXX | I-type (Immediate)
iiiiiiiiiiiiiiiiiiiiDDDDD11110XX | L-type (Long Immediate)
iiiiiiiiiiiiiiiiiiiiiiiii11111XX | D-type (Displacement)
```

**R-type**: The Register type instruction format specifies three registers: **RD** (destination), **RA** and **RB** (sources). The available opcode space is 16 bits.

**I-type**: The Immediate type instruction format specifies two registers, **RD** and **RS**, and a 12-bit immediate, **#imm**. The available opcode space is 9 bits.

**L-type**: The Long Immediate type instruction format specifies one register, **RD**, and a 20-bit immediate, **#limm**. The available opcode space is 2 bits.

**D-type**: The Displacement type instruction format specifies a sign-extended 25-bit immediate (left-shifted by 2), allowing for a displacement of +/-64 MiB. The available opcode space is 2 bits.
