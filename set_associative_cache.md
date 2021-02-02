# Set Associative Cache
### Problem

Consider a 3-way set-associative cache consisting of 16 bytes per block and 8 sets in total.
Answer the bit widths of the tags and indexes and the total number of bits in the entire cache.
Answer the tags, indexes, and hits or misses in the cache when referring to the addresses in the order shown in the table below.
Data replacement in the cache is done according to the LRU, and it is a write-through cache.

```
Bit width of index section=[  ]
Tag section bit width=[  ]
Total number of bits in the entire cache=[  ]
```

Fill in the table when the following address locus is accessed

<img width="275" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0009.png">

### Solution

- Bit width of index section
    - 8set = 2^3 = 3bit

- Tag section bit width
    - 1block = 16byte = 2^4 = 4bit			
    - Therefore, 32 - (3 + 4) = 25bit

- Total number of bits in the entire cache
    - [{block size(=16x8)} + 25(tag) + 1(valid flag)] x 8set x 3way = 154 x 8 x 3 = 3696bit

<img width="550" src="https://github.com/fffclaypool/study_computer_design/blob/images/Figure_0010.png">
