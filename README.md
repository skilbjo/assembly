# assembly

## run it

    src/run-file $file

file can be `binary`, ie the name of the exercise.
bash completion should fill in the details.

## Instruction Set

### Arithmetic and Logical Instructions

| Instruction | Opcode/Function |    Syntax    |          Operation         |
|:-----------:|:---------------:|:------------:|:--------------------------:|
|     add     |      100000     | f $d, $s, $t |        $d = $s + $t        |
|     addu    |      100001     | f $d, $s, $t |        $d = $s + $t        |
|     addi    |       1000      |  f $d, $s, i |       $d = $s + SE(i)      |
|    addiu    |       1001      |  f $d, $s, i |       $d = $s + SE(i)      |
|     and     |      100100     | f $d, $s, $t |        $d = $s & $t        |
|     andi    |       1100      |  f $d, $s, i |       $t = $s & ZE(i)      |
|     div     |      11010      |   f $s, $t   | lo = $s / $t; hi = $s % $t |
|     divu    |      11011      |   f $s, $t   | lo = $s / $t; hi = $s % $t |
|     mult    |      11000      |   f $s, $t   |       hi:lo = $s * $t      |
|    multu    |      11001      |   f $s, $t   |       hi:lo = $s * $t      |
|     nor     |      100111     | f $d, $s, $t |       $d = ~($s | $t)      |
|      or     |      100101     | f $d, $s, $t |        $d = $s | $t        |
|     ori     |       1101      |  f $d, $s, i |       $t = $s | ZE(i)      |
|     sll     |        0        |  f $d, $t, a |        $d = $t << a        |
|     sllv    |       100       | f $d, $t, $s |        $d = $t << $s       |
|     sra     |        11       |  f $d, $t, a |        $d = $t >> a        |
|     srav    |       111       | f $d, $t, $s |        $d = $t >> $s       |
|     srl     |        10       |  f $d, $t, a |        $d = $t >>> a       |
|     srlv    |       110       | f $d, $t, $s |       $d = $t >>> $s       |
|     sub     |      100010     | f $d, $s, $t |        $d = $s - $t        |
|     subu    |      100011     | f $d, $s, $t |        $d = $s - $t        |
|     xor     |      100110     | f $d, $s, $t |        $d = $s ^ $t        |
|     xori    |       1110      |  f $d, $s, i |       $d = $s ^ ZE(i)      |

### Constant-Manipulating Instructions

| Instruction | Opcode/Function |     Syntax    |  Operation  |
|:-----------:|:---------------:|:-------------:|:-----------:|
|     lhi     |      11001      | o $t, immed32 | HH ($t) = i |
|     llo     |      11000      | o $t, immed32 | LH ($t) = i |

### Comparison Instructions

| Instruction | Opcode/Function |    Syntax    |     Operation     |
|:-----------:|:---------------:|:------------:|:-----------------:|
|     slt     |      101010     | f $d, $s, $t |   $d = ($s < $t)  |
|     sltu    |      101001     | f $d, $s, $t |   $d = ($s < $t)  |
|     slti    |       1010      |  f $d, $s, i | $t = ($s < SE(i)) |
|    sltiu    |       1001      |  f $d, $s, i | $t = ($s < SE(i)) |

### Branch Instructions

| Instruction | Opcode/Function |      Syntax     |          Operation         |
|:-----------:|:---------------:|:---------------:|:--------------------------:|
|     beq     |       100       | o $s, $t, label | if ($s == $t) pc += i << 2 |
|     bgtz    |       111       |   o $s, label   |  if ($s > 0) pc += i << 2  |
|     blez    |       110       |   o $s, label   |  if ($s <= 0) pc += i << 2 |
|     bne     |       101       | o $s, $t, label | if ($s != $t) pc += i << 2 |

### Jump Instructions

| Instruction | Opcode/Function |  Syntax  |        Operation       |
|:-----------:|:---------------:|:--------:|:----------------------:|
|      j      |        10       |  o label |      pc += i << 2      |
|     jal     |        11       |  o label | $31 = pc; pc += i << 2 |
|     jalr    |       1001      | o labelR |    $31 = pc; pc = $s   |
|      jr     |       1000      | o labelR |         pc = $s        |

### Load Instructions

| Instruction | Opcode/Function |    Syntax    |         Operation        |
|:-----------:|:---------------:|:------------:|:------------------------:|
|      lb     |      100000     | o $t, i ($s) | $t = SE (MEM [$s + i]:1) |
|     lbu     |      100100     | o $t, i ($s) | $t = ZE (MEM [$s + i]:1) |
|      lh     |      100001     | o $t, i ($s) | $t = SE (MEM [$s + i]:2) |
|     lhu     |      100101     | o $t, i ($s) | $t = ZE (MEM [$s + i]:2) |
|      lw     |      100011     | o $t, i ($s) |    $t = MEM [$s + i]:4   |

### Store Instructions

| Instruction | Opcode/Function |    Syntax    |         Operation        |
|:-----------:|:---------------:|:------------:|:------------------------:|
|      sb     |      101000     | o $t, i ($s) | MEM [$s + i]:1 = LB ($t) |
|      sh     |      101001     | o $t, i ($s) | MEM [$s + i]:2 = LH ($t) |
|      sw     |      101011     | o $t, i ($s) |    MEM [$s + i]:4 = $t   |

### Data Movement Instructions

| Instruction | Opcode/Function | Syntax | Operation |
|:-----------:|:---------------:|:------:|:---------:|
|     mfhi    |      10000      |  f $d  |  $d = hi  |
|     mflo    |      10010      |  f $d  |  $d = lo  |
|     mthi    |      10001      |  f $s  |  hi = $s  |
|     mtlo    |      10011      |  f $s  |  lo = $s  |

### Exception and Interrupt Instructions

| Instruction | Opcode/Function | Syntax |                                  Operation                                  |
|:-----------:|:---------------:|:------:|:---------------------------------------------------------------------------:|
|     trap    |      11010      |   o i  | Dependent on OS; different values for immed26 specify different operations. |


### One table

|  Arithmetic and Logical Instructions |                 |                 |                                                                             |
|:------------------------------------:|:---------------:|:---------------:|:---------------------------------------------------------------------------:|
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                  add                 |      100000     |   f $d, $s, $t  |                                 $d = $s + $t                                |
|                 addu                 |      100001     |   f $d, $s, $t  |                                 $d = $s + $t                                |
|                 addi                 |       1000      |   f $d, $s, i   |                               $d = $s + SE(i)                               |
|                 addiu                |       1001      |   f $d, $s, i   |                               $d = $s + SE(i)                               |
|                  and                 |      100100     |   f $d, $s, $t  |                                 $d = $s & $t                                |
|                 andi                 |       1100      |   f $d, $s, i   |                               $t = $s & ZE(i)                               |
|                  div                 |      11010      |     f $s, $t    |                          lo = $s / $t; hi = $s % $t                         |
|                 divu                 |      11011      |     f $s, $t    |                          lo = $s / $t; hi = $s % $t                         |
|                 mult                 |      11000      |     f $s, $t    |                               hi:lo = $s * $t                               |
|                 multu                |      11001      |     f $s, $t    |                               hi:lo = $s * $t                               |
|                  nor                 |      100111     |   f $d, $s, $t  |                               $d = ~($s | $t)                               |
|                  or                  |      100101     |   f $d, $s, $t  |                                 $d = $s | $t                                |
|                  ori                 |       1101      |   f $d, $s, i   |                               $t = $s | ZE(i)                               |
|                  sll                 |        0        |   f $d, $t, a   |                                 $d = $t << a                                |
|                 sllv                 |       100       |   f $d, $t, $s  |                                $d = $t << $s                                |
|                  sra                 |        11       |   f $d, $t, a   |                                 $d = $t >> a                                |
|                 srav                 |       111       |   f $d, $t, $s  |                                $d = $t >> $s                                |
|                  srl                 |        10       |   f $d, $t, a   |                                $d = $t >>> a                                |
|                 srlv                 |       110       |   f $d, $t, $s  |                                $d = $t >>> $s                               |
|                  sub                 |      100010     |   f $d, $s, $t  |                                 $d = $s - $t                                |
|                 subu                 |      100011     |   f $d, $s, $t  |                                 $d = $s - $t                                |
|                  xor                 |      100110     |   f $d, $s, $t  |                                 $d = $s ^ $t                                |
|                 xori                 |       1110      |   f $d, $s, i   |                               $d = $s ^ ZE(i)                               |
|  Constant-Manipulating Instructions  |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                  lhi                 |      11001      |  o $t, immed32  |                                 HH ($t) = i                                 |
|                  llo                 |      11000      |  o $t, immed32  |                                 LH ($t) = i                                 |
|        Comparison Instructions       |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                  slt                 |      101010     |   f $d, $s, $t  |                                $d = ($s < $t)                               |
|                 sltu                 |      101001     |   f $d, $s, $t  |                                $d = ($s < $t)                               |
|                 slti                 |       1010      |   f $d, $s, i   |                              $t = ($s < SE(i))                              |
|                 sltiu                |       1001      |   f $d, $s, i   |                              $t = ($s < SE(i))                              |
|          Branch Instructions         |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                  beq                 |       100       | o $s, $t, label |                          if ($s == $t) pc += i << 2                         |
|                 bgtz                 |       111       |   o $s, label   |                           if ($s > 0) pc += i << 2                          |
|                 blez                 |       110       |   o $s, label   |                          if ($s <= 0) pc += i << 2                          |
|                  bne                 |       101       | o $s, $t, label |                          if ($s != $t) pc += i << 2                         |
|           Jump Instructions          |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                   j                  |        10       |     o label     |                                 pc += i << 2                                |
|                  jal                 |        11       |     o label     |                            $31 = pc; pc += i << 2                           |
|                 jalr                 |       1001      |     o labelR    |                              $31 = pc; pc = $s                              |
|                  jr                  |       1000      |     o labelR    |                                   pc = $s                                   |
|           Load Instructions          |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                  lb                  |      100000     |   o $t, i ($s)  |                           $t = SE (MEM [$s + i]:1)                          |
|                  lbu                 |      100100     |   o $t, i ($s)  |                           $t = ZE (MEM [$s + i]:1)                          |
|                  lh                  |      100001     |   o $t, i ($s)  |                           $t = SE (MEM [$s + i]:2)                          |
|                  lhu                 |      100101     |   o $t, i ($s)  |                           $t = ZE (MEM [$s + i]:2)                          |
|                  lw                  |      100011     |   o $t, i ($s)  |                             $t = MEM [$s + i]:4                             |
|          Store Instructions          |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                  sb                  |      101000     |   o $t, i ($s)  |                           MEM [$s + i]:1 = LB ($t)                          |
|                  sh                  |      101001     |   o $t, i ($s)  |                           MEM [$s + i]:2 = LH ($t)                          |
|                  sw                  |      101011     |   o $t, i ($s)  |                             MEM [$s + i]:4 = $t                             |
|      Data Movement Instructions      |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                 mfhi                 |      10000      |       f $d      |                                   $d = hi                                   |
|                 mflo                 |      10010      |       f $d      |                                   $d = lo                                   |
|                 mthi                 |      10001      |       f $s      |                                   hi = $s                                   |
|                 mtlo                 |      10011      |       f $s      |                                   lo = $s                                   |
| Exception and Interrupt Instructions |                 |                 |                                                                             |
|              Instruction             | Opcode/Function |      Syntax     |                                  Operation                                  |
|                 trap                 |      11010      |       o i       | Dependent on OS; different values for immed26 specify different operations. |
