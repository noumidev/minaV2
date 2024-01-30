# ADDH

**Add High**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111001` | `N/A`        | `L`      |

**Syntax**

```
    ADDH RD, #limm
```

**Description**: 20-bit immediate data is added to the upper 20 bits of **RD**.

**Operation**:

```
    RD += left_shift(#limm, 12)
```

**Exceptions**: None

# B (1)

**Branch**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111100` | `N/A`        | `D`      |

**Syntax**:

```
    B label
```

**Description**: The program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**.

**Operation**:

```
    IA = IA + left_shift(sign_extend(#disp), 2)
```

**Exceptions**: None

# B (2)

**Branch**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0111100` | `N/A`        | `R`      |

**Syntax**:

```
    B RD
```

**Description**: The program jumps to the address in the **RD** register.

**Operation**:

```
    IA = RD
```

**Exceptions**: None

# BL (1)

**Branch and Link**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111110` | `N/A`        | `D`      |

**Syntax**:

```
    BL label
```

**Description**: The program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```
    LA = IA + 4
    IA = IA + left_shift(sign_extend(#disp), 2)
```

**Exceptions**: None

# BL (2)

**Branch and Link**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0111110` | `N/A`        | `R`      |

**Syntax**:

```
    BL RD
```

**Description**: The program jumps to the address in the **RD** register. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```
    LA = IA + 4
    IA = RD
```

**Operand Restrictions**: **R31** cannot be specified for **RD**.

**Exceptions**: None

# BLT (1)

**Branch and Link if True**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111111` | `N/A`        | `D`      |

**Syntax**:

```
    BLT label
```

**Description**: When the T bit is set, the program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```
    LA = IA + 4

    if (T)
        IA = IA + left_shift(sign_extend(#disp), 2)
```

**Exceptions**: None

# BLT (2)

**Branch and Link if True**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0111111` | `N/A`        | `R`      |

**Syntax**:

```
    BLT RD
```

**Description**: When the T bit is set, the program jumps to the address in the **RD** register. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```
    LA = IA + 4

    if (T)
        IA = RD
```

**Operand Restrictions**: **R31** cannot be specified for **RD**.

**Exceptions**: None

# BT (1)

**Branch if True**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111101` | `N/A`        | `D`      |

**Syntax**:

```
    BT label
```

**Description**: When the T bit is set, the program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**.

**Operation**:

```
    if (T)
        IA = IA + left_shift(sign_extend(#disp), 2)
```

**Exceptions**: None

# BT (2)

**Branch if True**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0111101` | `N/A`        | `R`      |

**Syntax**:

```
    BT RD
```

**Description**: When the T bit is set, the program jumps to the address in the **RD** register.

**Operation**:

```
    if (T)
        IA = RD
```

**Exceptions**: None

# CEQ (1)

**Compare Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000000` | `I`      |

**Syntax**

```
    CEQ RA, #imm
```

**Description**: The T bit is set if **RA** is equal to the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RA == #imm)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CEQ (2)

**Compare Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001110` | `0000000000` | `R`      |

**Syntax**

```
    CEQ RA, RB
```

**Description**: The T bit is set if **RA** is equal to **RB**; otherwise, it is cleared.

**Operation**:

```
    if (RA == RB)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CGT (1)

**Compare Greater Than**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000011` | `I`      |

**Syntax**

```
    CGT RA, #imm
```

**Description**: The T bit is set if **RA** is greater than the sign-extended 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (signed(RA) > signed(sign_extend(#imm)))
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CGT (2)

**Compare Greater Than**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001110` | `0000000011` | `R`      |

**Syntax**

```
    CGT RA, RB
```

**Description**: The T bit is set if **RA** is greater than **RB**; otherwise, it is cleared. The registers are treated as signed.

**Operation**:

```
    if (signed(RA) > signed(RB))
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CHI (1)

**Compare Higher**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000001` | `I`      |

**Syntax**

```
    CHI RA, #imm
```

**Description**: The T bit is set if **RA** is greater than the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RA > #imm)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CHI (2)

**Compare Higher**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001110` | `0000000001` | `R`      |

**Syntax**

```
    CHI RA, RB
```

**Description**: The T bit is set if **RA** is greater than **RB**; otherwise, it is cleared. The registers are treated as unsigned.

**Operation**:

```
    if (RA > RB)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CLE (1)

**Compare Less Than or Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000111` | `I`      |

**Syntax**

```
    CLE RA, #imm
```

**Description**: The T bit is set if **RA** is less than or equal to the sign-extended 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (signed(RA) <= signed(sign_extend(#imm)))
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CLE (2)

**Compare Less Than or Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001110` | `0000000111` | `R`      |

**Syntax**

```
    CLE RA, RB
```

**Description**: The T bit is set if **RA** is less than or equal to **RB**; otherwise, it is cleared. The registers are treated as signed.

**Operation**:

```
    if (signed(RA) <= signed(RB))
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CLPB

**Clip Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000000` | `I`      |

**Syntax**

```
    CLPB RD, RA
```

**Description**: Register **RA** is clamped to the unsigned 8-bit integer range, the result is written to **RD**.

**Operation**

```
    if (RA > 0xFF)
        RA = 0xFF
    else
        RD = RA
```

**Exceptions**: None

# CLPBS

**Clip Byte Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000100` | `I`      |

**Syntax**

```
    CLPBS RD, RA
```

**Description**: Register **RA** is clamped to the signed 8-bit integer range, the result is written to **RD**.

**Operation**

```
    if (RA > 0x7F)
        RA = 0x7F
    else if (RA < -0x80)
        RA = -0x80
    else
        RD = RA
```

**Exceptions**: None

# CLPH

**Clip Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000001` | `I`      |

**Syntax**

```
    CLPH RD, RA
```

**Description**: Register **RA** is clamped to the unsigned 16-bit integer range, the result is written to **RD**.

**Operation**

```
    if (RA > 0xFFFF)
        RA = 0xFFFF
    else
        RD = RA
```

**Exceptions**: None

# CLPHS

**Clip Halfword Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000101` | `I`      |

**Syntax**

```
    CLPHS RD, RA
```

**Description**: Register **RA** is clamped to the signed 16-bit integer range, the result is written to **RD**.

**Operation**

```
    if (RA > 0x7FFF)
        RA = 0x7FFF
    else if (RA < -0x8000)
        RA = -0x8000
    else
        RD = RA
```

**Exceptions**: None

# CLS (1)

**Compare Lower Than or Same**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000101` | `I`      |

**Syntax**

```
    CLS RA, #imm
```

**Description**: The T bit is set if **RA** is less than or equal to the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RA <= #imm)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CLS (2)

**Compare Lower Than or Same**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001110` | `0000000101` | `R`      |

**Syntax**

```
    CLS RA, RB
```

**Description**: The T bit is set if **RA** is less than or equal to **RB**; otherwise, it is cleared. The registers are treated as unsigned.

**Operation**:

```
    if (RA <= RB)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CNE (1)

**Compare Not Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000100` | `I`      |

**Syntax**

```
    CNE RA, #imm
```

**Description**: The T bit is set if **RA** is not equal to the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RA != #imm)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# CNE (2)

**Compare Not Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001110` | `0000000100` | `R`      |

**Syntax**

```
    CNE RA, RB
```

**Description**: The T bit is set if **RA** is not equal to **RB**; otherwise, it is cleared.

**Operation**:

```
    if (RA != RB)
        T = 1
    else
        T = 0
```

**Exceptions**: None

# EXTB

**Extend Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001011` | `0000000000` | `I`      |

**Syntax**

```
    EXTB RD, RA
```

**Description**: The low 8 bits of register **RA** are zero-extended, the result is written to **RD**.

**Operation**

```
    RD = zero_extend(RA[7:0])
```

**Exceptions**: None

# EXTBS

**Extend Byte Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001011` | `0000000100` | `I`      |

**Syntax**

```
    EXTBS RD, RA
```

**Description**: The low 8 bits of register **RA** are sign-extended, the result is written to **RD**.

**Operation**

```
    RD = sign_extend(RA[7:0])
```

**Exceptions**: None

# EXTH

**Extend Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001011` | `0000000001` | `I`      |

**Syntax**

```
    EXTH RD, RA
```

**Description**: The low 16 bits of register **RA** are zero-extended, the result is written to **RD**.

**Operation**

```
    RD = zero_extend(RA[15:0])
```

**Exceptions**: None

# EXTHS

**Extend Halfword Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001011` | `0000000101` | `I`      |

**Syntax**

```
    EXTHS RD, RA
```

**Description**: The low 16 bits of register **RA** are sign-extended, the result is written to **RD**.

**Operation**

```
    RD = sign_extend(RA[15:0])
```

**Exceptions**: None

# LB (1)

**Load Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010000` | `0000000000` | `I`      |

**Syntax**

```
    LB RD, [RA, #imm]
```

**Description**: Byte data is zero-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    RD = read_byte(addr)
```

**Exceptions**: None

# LB (2)

**Load Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000000` | `R`      |

**Syntax**

```
    LB RD, [RA, RB]
```

**Description**: Byte data is zero-extended and read into register **RD**. The memory address is formed by adding **RB** to **RA**.

**Operation**:

```
    addr = RA + RB

    RD = read_byte(addr)
```

**Exceptions**: None

# LBS (1)

**Load Byte Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010000` | `0000000100` | `I`      |

**Syntax**

```
    LBS RD, [RA, #imm]
```

**Description**: Byte data is sign-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    RD = sign_extend(read_byte(addr))
```

**Exceptions**: None

# LBS (2)

**Load Byte Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000100` | `R`      |

**Syntax**

```
    LBS RD, [RA, RB]
```

**Description**: Byte data is sign-extended and read into register **RD**. The memory address is formed by adding **RB** to **RA**.

**Operation**:

```
    addr = RA + RB

    RD = sign_extend(read_byte(addr))
```

**Exceptions**: None

# LH (1)

**Load Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010000` | `0000000001` | `I`      |

**Syntax**

```
    LH RD, [RA, #imm]
```

**Description**: Halfword data is zero-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    if (addr[0] == 1)
        raise_exception(#ALI)

    RD = read_halfword(addr)
```

**Exceptions**: `#ALI` (Alignment Error)

# LH (2)

**Load Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000001` | `R`      |

**Syntax**

```
    LH RD, [RA, RB]
```

**Description**: Halfword data is zero-extended and read into register **RD**. The memory address is formed by adding **RB** to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RA + RB

    if (addr[0] == 1)
        raise_exception(#ALI)

    RD = read_halfword(addr)
```

**Exceptions**: `#ALI` (Alignment Error)

# LHS (1)

**Load Halfword Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010000` | `0000000101` | `I`      |

**Syntax**

```
    LHS RD, [RA, #imm]
```

**Description**: Halfword data is sign-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    if (addr[0] == 1)
        raise_exception(#ALI)

    RD = sign_extend(read_halfword(addr))
```

**Exceptions**: `#ALI` (Alignment Error)

# LHS (2)

**Load Halfword Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000101` | `R`      |

**Syntax**

```
    LHS RD, [RA, RB]
```

**Description**: Halfword data is sign-extended and read into register **RD**. The memory address is formed by adding **RB** to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RA + RB

    if (addr[0] == 1)
        raise_exception(#ALI)

    RD = sign_extend(read_halfword(addr))
```

**Exceptions**: `#ALI` (Alignment Error)

# LW (1)

**Load Word**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010000` | `0000000010` | `I`      |

**Syntax**

```
    LW RD, [RA, #imm]
```

**Description**: Word data is read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bits 0 and 1 of the address are not cleared.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    if (addr[1:0] != 0)
        raise_exception(#ALI)

    RD = read_word(addr)
```

**Exceptions**: `#ALI` (Alignment Error)

# LW (2)

**Load Word**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000010` | `R`      |

**Syntax**

```
    LW RD, [RA, RB]
```

**Description**: Word data is read into register **RD**. The memory address is formed by adding **RB** to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bits 0 and 1 of the address are not cleared.

**Operation**:

```
    addr = RA + RB

    if (addr[1:0] != 0)
        raise_exception(#ALI)

    RD = read_word(addr)
```

**Exceptions**: `#ALI` (Alignment Error)

# MFS

**Move From System**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1000100` | `N/A`        | `I`      |

**Syntax**

```
    MFS RD, #imm
```

**Description**: Data from the System Register with number `#imm` is written to register **RD**.

**Operation**:

```
    RD = read_sr(#imm)
```

**Exceptions**: `#PRV` (Privilege Error)

# MOVH

**Move High**

```
31                        6     0
 iiiiiiiiiiiiiiiiiiiiDDDDD1111000
```

**Syntax**

```
    MOVH RD, #limm
```

**Description**: 20-bit immediate data is written to the upper 20 bits of **RD**. The lower 12 bits of **RD** are cleared.

**Operation**:

```
    RD = left_shift(#limm, 12)
```

**Exceptions**: None

# MTS

**Move To System**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1000101` | `N/A`        | `I`      |

**Syntax**

```
    MTS RD, #imm
```

**Description**: Register **RD** is written to the System Register with number `#imm`.

**Operation**:

```
    write_sr(#imm, RD)
```

**Exceptions**: `#PRV` (Privilege Error)

# ORH

**Bitwise OR High**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111010` | `N/A`        | `L`      |

**Syntax**

```
    ORH RD, #limm
```

**Description**: The upper 20 bits of **RD** are ORed with 20-bit immediate data.

**Operation**:

```
    RD |= left_shift(#limm, 12)
```

**Exceptions**: None

# SB (1)

**Store Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010001` | `0000000000` | `I`      |

**Syntax**

```
    SB RD, [RA, #imm]
```

**Description**: The low 8 bits of **RD** are written to memory. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    write_byte(addr, RD[7:0])
```

**Exceptions**: None

# SB (2)

**Store Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000000` | `R`      |

**Syntax**

```
    SB RD, [RA, RB]
```

**Description**: The low 8 bits of **RD** are written to memory. The memory address is formed by adding **RB** to **RA**.

**Operation**:

```
    addr = RA + RB

    write_byte(addr, RD[7:0])
```

**Exceptions**: None

# SEL

**Select**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001111` | `N/A`        | `R`      |

**Syntax**

```
    SEL RD, RA, RB
```

**Description**: When the T bit is set, **RA** is written to **RD**; otherwise, **RB** is written to **RD**.

**Operation**:

```
    if (T)
        RD = RA
    else
        RD = RB
```

**Exceptions**: None

# SH (1)

**Store Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010001` | `0000000001` | `I`      |

**Syntax**

```
    SH RD, [RA, #imm]
```

**Description**: The low 16 bits of **RD** are written to memory. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    if (addr[0] == 1)
        raise_exception(#ALI)

    write_halfword(addr, RD[15:0])
```

**Exceptions**: `#ALI` (Alignment Error)

# SH (2)

**Store Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010000` | `0000000001` | `R`      |

**Syntax**

```
    SH RD, [RA, RB]
```

**Description**: The low 16 bits of **RD** are written to memory. The memory address is formed by adding **RB** to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RA + RB

    if (addr[0] == 1)
        raise_exception(#ALI)

    write_halfword(addr, RD[15:0])
```

**Exceptions**: `#ALI` (Alignment Error)

# SW (1)

**Store Word**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010001` | `0000000010` | `I`      |

**Syntax**

```
    SW RD, [RA, #imm]
```

**Description**: Register **RD** is written to memory. The memory address is formed by adding sign-extended 12-bit immediate data to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bits 0 and 1 of the address are not cleared.

**Operation**:

```
    addr = RA + sign_extend(#imm)

    if (addr[1:0] != 0)
        raise_exception(#ALI)

    write_word(addr, RD)
```

**Exceptions**: `#ALI` (Alignment Error)

# SW (2)

**Store Word**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0010001` | `0000000010` | `R`      |

**Syntax**

```
    SW RD, [RA, RB]
```

**Description**: Register **RD** are written to memory. The memory address is formed by adding **RB** to **RA**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bits 0 and 1 of the address are not cleared.

**Operation**:

```
    addr = RA + RB

    if (addr[1:0] != 0)
        raise_exception(#ALI)

    write_word(addr, RD)
```

**Exceptions**: `#ALI` (Alignment Error)

# SYSCALL

**System Call**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0000001` | `N/A`        | `R`      |

**Syntax**:

```
    SYSCALL
```

**Description**: A system call exception occurs.

**Operation**:

```
    raise_exception(#SYS);
```

**Exceptions**: `#SYS` (System Call)

# UDF

**Undefined**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0000000` | `N/A`        | `R`      |

**Syntax**:

```
    UDF
```

**Description**: An undefined instruction exception occurs.

**Operation**:

```
    raise_exception(#UDF);
```

**Exceptions**: `#UDF` (Undefined Instruction)

# XORH

**Bitwise Exclusive OR High**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1111011` | `N/A`        | `L`      |

**Syntax**

```
    XORH RD, #limm
```

**Description**: The upper 20 bits of **RD** are XORed with 20-bit immediate data.

**Operation**:

```
    RD ^= left_shift(#limm, 12)
```

**Exceptions**: None
