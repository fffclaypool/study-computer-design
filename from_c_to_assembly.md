# Converting C language to MIPS assembly language
### Overview

Show the following algorithms in MIPS assembly language.

Conditional branches are shown as numbers, not labels. The instruction sequence start with 100hex.

### Problem 1
##### Algorithm

```C
for( i = 0; i != 10; i++ ){
    sum += data[i];
}
```

i=$t0, data=$s0; sum = $s1.

##### Assembly

```
100 add $t0, $zero, $zero   # Initialize i.
104 addi $t1, $zero, 10     # Define 10 to be compared to i.
108 beq $t0, $t1, ????      # If i = 10, return to ????.
10c sll $t2, $t0, 2         # Multiply $t0 by 4 because of pointing memory address.
110 add $t2, $t2, $s0       # Add $t2 and $s0.
114 lw $t3, 0($t2)          # Load the data at $t2.
118 add $s1, $s1, $t3       # Add $s1 and $t3.
11c addi $t0, $t0, 1        # Add $t0 and 1.
120 beq $zero, $zero, -7    # Jump to 108.
```

### Problem 2
##### Algorithm

```C
if( data[i] < data[i+1] )
    data[i]=0;
else
    data[i] = data[i+1];
return( i );
```

i=$a1, data=$a0; the return value should be returned to $v0.

##### Assembly

```
100 sll $t1, $a1, 2     # Multiply $a1 by 4 because of pointing memory address.
104 add $t1, $t1, $a0   # Add $t1 and $a0.
108 lw $t2, 0($t1)      # Load the data at $t1.
10c lw $t3, 4($t1)      # Load the data at $t1+4.
110 slt $t4, $t2, $t3   # Determine if $t2 is less than $t3.
114 beq $t4, $zero, 2   # if $t4 = 0, jump to 120
118 sw $zero, 0($t1)    # Store 0 at $t1.
11c beq $zero, $zero, 1 # Jump to 124.
120 sw $t3, 0($t2)      # Store $t2 at $t3.
124 addi $v0, $a1, 0    # Add $a1 and 0.
```