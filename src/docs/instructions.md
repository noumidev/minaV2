# B (1)

**Branch**

```
31                        6     0
 iiiiiiiiiiiiiiiiiiiiiiiii1111100
```

**Syntax**:

```
    B label
```

**Description**: The program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**.

**Operation**:

```c
    IA = IA + left_shift(sign_extend(#disp), 2)
```

**Exceptions**: None

# B (2)

**Branch**

```
31                        6     0
 00000000000000000000DDDDD0111100
```

**Syntax**:

```
    B RD
```

**Description**: The program jumps to the address in the **RD** register.

**Operation**:

```c
    IA = RD
```

**Exceptions**: None

# BL (1)

**Branch and Link**

```
31                        6     0
 iiiiiiiiiiiiiiiiiiiiiiiii1111110
```

**Syntax**:

```
    BL label
```

**Description**: The program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```c
    LA = IA + 4
    IA = IA + left_shift(sign_extend(#disp), 2)
```

**Exceptions**: None

# BL (2)

**Branch and Link**

```
31                        6     0
 00000000000000000000DDDDD0111110
```

**Syntax**:

```
    BL RD
```

**Description**: The program jumps to the address in the **RD** register. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```c
    LA = IA + 4
    IA = RD
```

**Operand Restrictions**: **R31** cannot be specified for **RD**.

**Exceptions**: None

# BLT (1)

**Branch and Link if True**

```
31                        6     0
 iiiiiiiiiiiiiiiiiiiiiiiii1111111
```

**Syntax**:

```
    BLT label
```

**Description**: When the T bit is set, the program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```c
    LA = IA + 4

    if (PSTATE.T)
        IA = IA + left_shift(sign_extend(#disp), 2)
    endif
```

**Exceptions**: None

# BLT (2)

**Branch and Link if True**

```
31                        6     0
 00000000000000000000DDDDD0111111
```

**Syntax**:

```
    BLT RD
```

**Description**: When the T bit is set, the program jumps to the address in the **RD** register. The address of the following instruction is stored in **R31** (Link Address).

**Operation**:

```c
    LA = IA + 4

    if (PSTATE.T)
        IA = RD
    endif
```

**Operand Restrictions**: **R31** cannot be specified for **RD**.

**Exceptions**: None

# BT (1)

**Branch if True**

```
31                        6     0
 iiiiiiiiiiiiiiiiiiiiiiiii1111101
```

**Syntax**:

```
    BT label
```

**Description**: When the T bit is set, the program jumps to the destination address. The destination address is formed by left-shifting the sign-extended 25-bit displacement two bits and adding it to **IA**.

**Operation**:

```c
    if (PSTATE.T)
        IA = IA + left_shift(sign_extend(#disp), 2)
    endif
```

**Exceptions**: None

# BT (2)

**Branch if True**

```
31                        6     0
 00000000000000000000DDDDD0111101
```

**Syntax**:

```
    BT RD
```

**Description**: When the T bit is set, the program jumps to the address in the **RD** register.

**Operation**:

```c
    if (PSTATE.T)
        IA = RD
    endif
```

**Exceptions**: None
