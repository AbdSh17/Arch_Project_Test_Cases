# Arch Project Test Cases
this file contains Assembly codes with their coresponding HEX. value and the final resault


## EX1)
#### test basic functionallity
`ADDI R1, R1, 5`: `14440005` </br>
`SW R1, [R0 + 1]`: `1C400001` </br>
`ADDI R0, 1`: `14000001` </br>
BZ R6, -4: 28CCFFFD

Final Value: the loop will continue storing 5, a, f, 10....

## EX2)  
#### Test basic branch with LDW, SDW and their hazard detection: 
`ADDI R1, R1, 5`: `14440005` </br>
`SW R1, [R0 + 0]`: `1C400000` </br>
`ADDI R0, 1`: `14000001` </br>
SWD R0, [R0 + 1]: 24000001
ADDI R2, R0, -3: 14803FFD
BLZ R2, -6: 30083FFA
LWD R0, [R0 + 0]: 20000000
SWD R0, [R0 + 4]: 24000004

Final Resault:

MEM[0]: 5
MEM[1]: 10
MEM[2]: 15
MEM[3]: 2
MEM[4]: 3
MEM[5]: 15
MEM[6]: 2
MEM[7]: 3

## EX3) **
#### Important one: test hazard detection for when ODD:
`ADDI R1, R1, 5`: `14440005` </br>
`SW R1, [R0 + 0]`: `1C400000` </br>
`ADDI R0, 1`: `14000001` </br>
SWD R0, [R0 + 1]: 24000001
ADDI R2, R0, -3: 14803FFD
BLZ R2, -6: 30083FFA
LWD R0, [R0 + 0]: 20000000
LWD R1, [R0 + 0]: 20400000
SWD R0, [R0 + 4]: 24000004

Final Resault:

MEM[0]: 5
MEM[1]: 10
MEM[2]: 15
MEM[3]: 2
MEM[4]: 3
MEM[5]: 15
MEM[6]: 2
MEM[7]: 3

## EX4)
#### Test nested loops

ADDI R6, 3 15980003
ADDI R5, 3 15540003
ADDI R1, R1, 5 14440005
SW R1, [R0 + 0], 1C400000
ADDI R0, 1, 14000001
SW R0, [R0 + 1], 1C000000
ADDI R5, -1 15543FFF
BGZ R5, -3, 2C143FFD 
ADDI R0, 1, 14000001
ADDI, R6, -1, 15983FFF
BGZ R6,-9 2C183FF7
