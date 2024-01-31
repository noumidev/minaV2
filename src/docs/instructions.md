# ADD (1)

**Add**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001000` | `0000000000` | `I`      |

**Syntax**

```
    ADD RD, RS, #imm
```

**Description**: 12-bit immediate data is added to register **RS**, the result is written to **RD**. 

**Operation**:

```
    RD = RS + #imm
```

**Exceptions**: None

# ADD (2)

**Add**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000000` | `R`      |

**Syntax**

```
    ADD RD, RA, RB
```

**Description**: Register **RA** is added to **RB**, the result is written to **RD**. 

**Operation**:

```
    RD = RA + RB
```

**Exceptions**: None

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

# AND (1)

**Bitwise AND**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001000` | `0000000110` | `I`      |

**Syntax**

```
    AND RD, RS, #imm
```

**Description**: Register **RS** is ANDed with 12-bit immediate data, the result is written to **RD**. 

**Operation**:

```
    RD = RS & #imm
```

**Exceptions**: None

# AND (2)

**Bitwise AND**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000110` | `R`      |

**Syntax**

```
    AND RD, RA, RB
```

**Description**: Register **RA** is ANDed with **RB**, the result is written to **RD**. 

**Operation**:

```
    RD = RA & RB
```

**Exceptions**: None

# ANDN (1)

**Bitwise AND NOT**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001000` | `0000000111` | `I`      |

**Syntax**

```
    ANDN RD, RS, #imm
```

**Description**: Register **RS** is ANDed with the complement of 12-bit immediate data, the result is written to **RD**. 

**Operation**:

```
    RD = RS & ~(#imm)
```

**Exceptions**: None

# ANDN (2)

**Bitwise AND NOT**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000111` | `R`      |

**Syntax**

```
    ANDN RD, RA, RB
```

**Description**: Register **RA** is ANDed with the complement of **RB**, the result is written to **RD**. 

**Operation**:

```
    RD = RA & ~RB
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
    CEQ RS, #imm
```

**Description**: The T bit is set if **RS** is equal to the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RS == #imm)
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
    CGT RS, #imm
```

**Description**: The T bit is set if **RS** is greater than the sign-extended 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (signed(RS) > signed(sign_extend(#imm)))
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
    CHI RS, #imm
```

**Description**: The T bit is set if **RS** is greater than the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RS > #imm)
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
    CLE RS, #imm
```

**Description**: The T bit is set if **RS** is less than or equal to the sign-extended 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (signed(RS) <= signed(sign_extend(#imm)))
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

# CLO

**Count Leading 1s**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001001` | `0000000011` | `I`      |

**Syntax**

```
    CLO RD, RS
```

**Description**: The leading 1-bits in register **RS** are counted, the result is written to **RD**.

**Operation**:

```
    RD = count_leading_ones(RS)
```

**Exceptions**: None

# CLPB

**Clip Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000000` | `I`      |

**Syntax**

```
    CLPB RD, RS
```

**Description**: Register **RS** is clamped to the unsigned 8-bit integer range, the result is written to **RD**.

**Operation**

```
    if (RS > 0xFF)
        RD = 0xFF
    else
        RD = RS
```

**Exceptions**: None

# CLPBS

**Clip Byte Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000100` | `I`      |

**Syntax**

```
    CLPBS RD, RS
```

**Description**: Register **RS** is clamped to the signed 8-bit integer range, the result is written to **RD**.

**Operation**

```
    if (signed(RS) > signed(0x7F))
        RD = 0x7F
    else if (signed(RS) < signed(0xFFFFFF80))
        RD = 0xFFFFFF80
    else
        RD = RS
```

**Exceptions**: None

# CLPH

**Clip Halfword**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000001` | `I`      |

**Syntax**

```
    CLPH RD, RS
```

**Description**: Register **RS** is clamped to the unsigned 16-bit integer range, the result is written to **RD**.

**Operation**

```
    if (RS > 0xFFFF)
        RD = 0xFFFF
    else
        RD = RS
```

**Exceptions**: None

# CLPHS

**Clip Halfword Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001010` | `0000000101` | `I`      |

**Syntax**

```
    CLPHS RD, RS
```

**Description**: Register **RS** is clamped to the signed 16-bit integer range, the result is written to **RD**.

**Operation**

```
    if (signed(RA) > signed(0x7FFF))
        RD = 0x7FFF
    else if (signed(RA) < signed(0xFFFF8000))
        RD = 0xFFFF8000
    else
        RD = RS
```

**Exceptions**: None

# CLS (1)

**Compare Lower Than or Same**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000101` | `I`      |

**Syntax**

```
    CLS RS, #imm
```

**Description**: The T bit is set if **RS** is less than or equal to the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RS <= #imm)
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

# CLZ

**Count Leading 0s**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001001` | `0000000010` | `I`      |

**Syntax**

```
    CLZ RD, RS
```

**Description**: The leading 0-bits in register **RS** are counted, the result is written to **RD**.

**Operation**:

```
    RD = count_leading_zeros(RS)
```

**Exceptions**: None

# CNE (1)

**Compare Not Equal**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001110` | `0000000100` | `I`      |

**Syntax**

```
    CNE RS, #imm
```

**Description**: The T bit is set if **RS** is not equal to the unsigned 12-bit immediate data; otherwise, it is cleared.

**Operation**:

```
    if (RS != #imm)
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

# EXT

**Extract**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001100` | `0000000000` | `R*`     |

**Syntax**

```
    EXT RD, RA, #size, #shift
```

**Description**: Register **RA** is right-shifted `#shift` bits, the first `#size` bits of the result are zero-extended and written to **RD**. A `#size` of 0 encodes the value 32.

**Operation**:

```
    #size = secopc[4:0]
    if (#size == 0)
        #size = 32
    
    #shift = secopc[9:5]

    RD = zero_extend(right_shift(RA, #shift)[#size-1:0])
```

**Exceptions**: None

# EXTS

**Extract Signed**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001100` | `0000000100` | `R*`     |

**Syntax**

```
    EXTS RD, RA, #size, #shift
```

**Description**: Register **RA** is right-shifted `#shift` bits, the first `#size` bits of the result are sign-extended and written to **RD**. A `#size` of 0 encodes the value 32.

**Operation**:

```
    #size = secopc[4:0]
    if (#size == 0)
        #size = 32
    
    #shift = secopc[9:5]

    RD = sign_extend(right_shift(RA, #shift)[#size-1:0])
```

**Exceptions**: None

# INS

**Insert**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001100` | `0000000001` | `R*`     |

**Syntax**

```
    INS RD, RA, RB, #size, #shift
```

**Description**: The first `#size` bits of register **RB** are left-shifted `#shift` bits and inserted in **RA**, the result is written to **RD**. A `#size` of 0 encodes the value 32.

**Operation**:

```
    #size = secopc[4:0]
    if (#size == 0)
        #size = 32
    
    #shift = secopc[9:5]

    RD = {RA[31:#size+#shift], left_shift(RB[#size-1:0], #shift), RA[#shift-1:0]}
```

**Exceptions**: None

# INSZ

**Insert Zero**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001100` | `0000000011` | `R*`     |

**Syntax**

```
    INSZ RD, RB, #size, #shift
```

**Description**: The first `#size` bits of register **RB** are left-shifted `#shift` bits, the zero-extended result is written to **RD**. A `#size` of 0 encodes the value 32.

**Operation**:

```
    #size = secopc[4:0]
    if (#size == 0)
        #size = 32
    
    #shift = secopc[9:5]

    RD = zero_extend(left_shift(RB[#size-1:0], #shift))
```

**Exceptions**: None

# LB (1)

**Load Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010000` | `0000000000` | `I`      |

**Syntax**

```
    LB RD, [RS, #imm]
```

**Description**: Byte data is zero-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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
    LBS RD, [RS, #imm]
```

**Description**: Byte data is sign-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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
    LH RD, [RS, #imm]
```

**Description**: Halfword data is zero-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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
    LHS RD, [RS, #imm]
```

**Description**: Halfword data is sign-extended and read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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
    LW RD, [RS, #imm]
```

**Description**: Word data is read into register **RD**. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bits 0 and 1 of the address are not cleared.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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

# MAC

**Multiply-Accumulate**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001101` | `0000000010` | `R`      |

**Syntax**

```
    MAC RD, RA, RB
```

**Description**: Register **RA** is multiplied by **RB**, the result is added to **RD**. 

**Operation**:

```
    RD = RA * RB + RD
```

**Exceptions**: None

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
    if (has_privilege())
        RD = read_sr(#imm)
    else
        raise_exception(#PRV)
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

# MOVN

**Move NOT**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000011` | `R`      |

**Syntax**

```
    MOVN RD, RB
```

**Description**: The complement of register **RB** is written to **RD**. 

**Operation**:

```
    RD = ~RB
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
    if (has_privilege())
        write_sr(#imm, RD)
    else
        raise_exception(#PRV)
```

**Exceptions**: `#PRV` (Privilege Error)

# MUL

**Multiply**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001101` | `0000000000` | `R`      |

**Syntax**

```
    MUL RD, RA, RB
```

**Description**: Register **RA** is multiplied by **RB**, the result is written to **RD**. 

**Operation**:

```
    RD = RA * RB
```

**Exceptions**: None

# MULF

**Multiply Fixed-Point**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001101` | `0000000001` | `R`      |

**Syntax**

```
    MULF RD, RA, RB
```

**Description**: Register **RA** is multiplied by **RB**, bits 47-16 of the result are written to **RD**. 

**Operation**:

```
    RD = (RA * RB)[47:16]
```

**Exceptions**: None

# NEG

**Negate**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000010` | `R`      |

**Syntax**

```
    NEG RD, RB
```

**Description**: The 2's complement of register **RB** is written to **RD**. 

**Operation**:

```
    RD = -RB
```

**Exceptions**: None

# OR (1)

**Bitwise OR**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001000` | `0000000100` | `I`      |

**Syntax**

```
    OR RD, RS, #imm
```

**Description**: Register **RS** is ORed with 12-bit immediate data, the result is written to **RD**. 

**Operation**:

```
    RD = RS | #imm
```

**Exceptions**: None

# OR (2)

**Bitwise OR**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000100` | `R`      |

**Syntax**

```
    OR RD, RA, RB
```

**Description**: Register **RA** is ORed with **RB**, the result is written to **RD**. 

**Operation**:

```
    RD = RA | RB
```

**Exceptions**: None

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

# REV

**Reverse**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001001` | `0000000000` | `I`      |

**Syntax**

```
    REV RD, RS
```

**Description**: The bits in register **RS** are reversed, the result is written to **RD**.

**Operation**:

```
    RD = reverse_bits(RS)
```

**Exceptions**: None

# ROR (1)

**Rotate Right**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001011` | `N/A`        | `I`      |

**Syntax**

```
    ROR RD, RS, #imm
```

**Description**: Register **RS** is right-rotated `#imm` bits, the result is written to **RD**. The shift amount is masked to 5 bits.

**Operation**:

```
    RD = rotate_right(RS, #imm[4:0])
```

**Exceptions**: None

# ROR (2)

**Rotate Right**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001011` | `N/A`        | `R`      |

**Syntax**

```
    ROR RD, RA, RB
```

**Description**: Register **RA** is right-rotated **RB** bits, the result is written to **RD**. The shift amount is masked to 5 bits.

**Operation**:

```
    RD = rotate_right(RA, RB[4:0])
```

**Exceptions**: None

# SB (1)

**Store Byte**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010001` | `0000000000` | `I`      |

**Syntax**

```
    SB RD, [RS, #imm]
```

**Description**: The low 8 bits of **RD** are written to memory. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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
    SH RD, [RS, #imm]
```

**Description**: The low 16 bits of **RD** are written to memory. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bit 0 of the address is not cleared.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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

# SUB (1)

**Subtract**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001000` | `0000000001` | `I`      |

**Syntax**

```
    SUB RD, RS, #imm
```

**Description**: 12-bit immediate data is subtracted from register **RS**, the result is written to **RD**. 

**Operation**:

```
    RD = RS - #imm
```

**Exceptions**: None

# SUB (2)

**Subtract**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000001` | `R`      |

**Syntax**

```
    SUB RD, RA, RB
```

**Description**: Register **RB** is subtracted from **RA**, the result is written to **RD**. 

**Operation**:

```
    RD = RA - RB
```

**Exceptions**: None

# SW (1)

**Store Word**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1010001` | `0000000010` | `I`      |

**Syntax**

```
    SW RD, [RS, #imm]
```

**Description**: Register **RD** is written to memory. The memory address is formed by adding sign-extended 12-bit immediate data to **RS**.

**Alignment**: Implementations that do not support unaligned memory accesses raise an Alignment Error exception if bits 0 and 1 of the address are not cleared.

**Operation**:

```
    addr = RS + sign_extend(#imm)

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

# SWPB

**Swap Bytes**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001001` | `0000000100` | `I`      |

**Syntax**

```
    SWPB RD, RS
```

**Description**: The byte order of register **RS** is reversed, the result is written to **RD**.

**Operation**:

```
    RD = {RS[7:0], RS[15:8], RS[23:16], RS[31:24]}
```

**Exceptions**: None

# SWPH

**Swap Halfwords**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001001` | `0000000101` | `I`      |

**Syntax**

```
    SWPH RD, RS
```

**Description**: The halfword order of register **RS** is reversed, the result is written to **RD**.

**Operation**:

```
    RD = {RS[15:0], RS[31:16]}
```

**Exceptions**: None

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

# XOR (1)

**Bitwise XOR**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `1001000` | `0000000101` | `I`      |

**Syntax**

```
    XOR RD, RS, #imm
```

**Description**: Register **RS** is XORed with 12-bit immediate data, the result is written to **RD**. 

**Operation**:

```
    RD = RS ^ #imm
```

**Exceptions**: None

# XOR (2)

**Bitwise XOR**

| Opcode    | Secondary    | Encoding |
|-----------|--------------|----------|
| `0001000` | `0000000101` | `R`      |

**Syntax**

```
    XOR RD, RA, RB
```

**Description**: Register **RA** is XORed with **RB**, the result is written to **RD**. 

**Operation**:

```
    RD = RA | RB
```

**Exceptions**: None

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
