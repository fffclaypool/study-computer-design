# Values of the signal lines in the MIPS architecture
### Problem

Consider the following CPU. The initial state is PC=00000100hex, and the content of register number n is 2n. The content of memory address m is m+1.
When ClockCycle=1, it is assumed that the first instruction is being executed in the IF Stage.
Answer the value of the signal line when the following instruction sequence is executed.

<img width="839" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0001.png">

##### Assembly

```
add $s3, $t1, $s4
and $s3, $t1, $s3
lw $s4, 22ten($s3)
lw $s5, 23ten($s4)
add $s3, $s4, $s5
sw $s3, 23ten($s5)
sub $s3, $s5, $s3
```

##### When ClockCycle=5

```
ID/EX.RegDst=[  ]
EX/MEM.MemtoReg=[  ]
ForwardA=[  ]
ForwardB=[  ]
A=[  ]
G=[  ]
H=[  ]
J=[  ]
N=[  ]
P=[  ]
T=[  ]
```

##### When ClockCycle=8

```
ID/EX.MemtoReg=[  ]
EX/MEM.MemtoReg=[  ]
MEM/WB.MemtoReg=[  ]
B=[  ]
D=[  ]
K=[  ]
L=[  ]
R=[  ]
S=[  ]
```

### Solution

<img width="698" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0002.png">

<img width="598" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0003.png">

##### When ClockCycle=5

- ID/EX.RegDst
    - ID/EX.RegDst is lw.RegDst
    - Therefore, ID/EX.RegDst = 0

- EX/MEM.MemtoReg
    - EX/MEM.MemtoReg is and.MemtoReg
    - Therefore, EX/MEM.MemtoReg = 0

- ForwardA
    - The first operand of the ALU is sent from the result of the previous ALU
    - Therefore, ForwardA = 10

- ForwardB
    - The second operand of the ALU is obtained from the register files
    - Therefore, ForwardB = 00

- A
    - A is a value of read data 1 in ID
    - Therefore, A = $s4 = 18 + 22 = 40ten

- G
    - G is a value of the ALU result in EX
    - Therefore, G = 18 + 22 = 40ten

- H
    - H is a value sent from the result of the two previous ALU
    - Therefore, H = ForwardA = 18 + 40 = 58ten

- J
    - J is a value sent from the result of the previous ALU
    - Therefore, J = 18ten = 00000012hex

- N
    - N is a value that is sign-extended and logically shifted 2 bits to the left in ID
    - Therefore, N = 23 x 4 = 92ten

- P
    - P = H
    - Therefore, H = 58ten

- T
    - T is a value of PC + 4(ten) in IF
    - Therefore, T = 00000100hex + 00000014hex  = 00000114hex


##### When ClockCycle=8

- ID/EX.MemtoReg
    - ID/EX is bubble2
    - Therefore, ID/EX.MemtoReg = 0

- EX/MEM.MemtoReg
    - EX/MEM.MemtoReg is lw.MemtoReg
    - Therefore, EX/MEM.MemtoReg = 1

- MEM/WB.MemtoReg
    - MEM/WB is bubble1
    - Therefore, MEM/WB.MemtoReg = 0

- B
    - B is a value of read data 2 in ID
    - Therefore, B = 21 x 2 = 42ten

- D
    - D is a value of read data 1 in EX
    - Therefore, D = 41ten

- K
    - K = lw.instruction[20-16]
    - Therefore, K = 21ten

- L
    - L is a value of the ALU result in MEM
    - Therefore, L = 23 + 41 = 64ten

- R
    - R is a resulting value of MUX at position K in WB
    - Therefore, R = 21ten

- S
    - S = PChex + 4hex + [Value after logical shift of 2 bits to the left]hex
    - Therefore, S = ffe6194hex


### References
##### Single-Cycle Datapath and Control Specification

<img width="602" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0004.png">

##### R-format Instructions

<img width="660" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0005.png">

##### I-format Instructions

<img width="662" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0006.png">

##### J-format Instructions

<img width="659" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0007.png">

##### Register Numbers and Register Names

<img width="475" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0008.png">
