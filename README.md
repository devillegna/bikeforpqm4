
# BIKE KEM implenetations on Arm Cortex-M4

## There are 4 implementatins in 4 directories:
- bikel1portable : BIKE level 1, implementation from BIKE team, adapted from supercop-20200906/crypto_kem/bikel1/portable/ .
- bikel3portable : BIKE level 3, implementation from BIKE team, adapted from supercop-20200906/crypto_kem/bikel3/portable/ .  
- bikel1m4 : BIKE level 1, this work, modified from BIKE team's portable version.
- bikel3m4 : BIKE level 3, this work, modified from BIKE team's portable version.

  portablel1 and portablel3 were adapted from the BIKE team's portable implementation in SUPERCOP.
  Specifically, we changed line 29 and 30 in sampling_portable.c to  

<   uint32_t pos_qw[MAX_WLIST_SIZE];  
<   uint64_t pos_bit[MAX_WLIST_SIZE];  
from  
>   size_t pos_qw[MAX_WLIST_SIZE];  
>   size_t pos_bit[MAX_WLIST_SIZE];  

  The original implementation presumed size_t a 64-bit data type, which is not true in 32-bit machines.


## Instructions for benchmarking on PQM4
1. *Download* and *Setup* benchmarking environment for PQM4 from https://github.com/mupq/pqm4 .
2. Copy the *imple*/ directory to  *pqm4*/crypto_kem/*your_desired_name*/ . For example,  
  'cp -r crypto_kem/bikel1m4  *pqm4*/crypto_kem/bikel1m4'  
  assuming the PQM4 is installed in the *pqm4* directory.  
3. Use standard tester on PQM4 for the implementation you copied. For example, in the *pqm4* directory, execute  
  'python3 test.py'  
  or  
  'make IMPLEMENTATION_PATH=crypto_kem/bikel1m4 bin/crypto_kem_bikel1m4_speed.bin; st-flash write bin/crypto_kem_bikel1m4_speed.bin 0x8000000' .  
  Then collect benchmark results from the UART port of your M4 board with tools from PQM4 .  

