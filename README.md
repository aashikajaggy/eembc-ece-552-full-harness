# EEMBC ECE 552 Full Harness
The verilator-and-hamming branch contains ...
- modifications for the hamming distance calculation
- modifications to the EEMBC benchmark to compute output table, metric table (PRE-ACS), perform ACS loop with Verilated RTL, and traceback
- Verilated RTL files in a folder called `obj_dir` in `ece-552-viterbi-decoder/viterb00`

# Requirements to test
Need to install Verilator, I followed the guide here (I recommend using an ubuntu VM):
https://verilator.org/guide/latest/install.html

Once verilator is set up, then you can run the tests with gett, toggle, zeros, and ones.
Here are the commands I used: 
```
cd ece-552-viterbi-decoder/viterb00/test   # adjust to wherever the repo lives on the VM
chmod +x build_bench_hw_vm.sh              # once, if it isn't already executable

./build_bench_hw_vm.sh 1    # gett    (expect CRC 0x79f0)
./build_bench_hw_vm.sh 2    # toggle  (expect CRC 0x096a)
./build_bench_hw_vm.sh 3    # ones    (expect CRC 0x48bf)
./build_bench_hw_vm.sh 4    # zeros   (expect CRC 0x0000)
```

You should see a "DONE!" if the tests pass. 

#Important files to look at
- viterb00.c : where all of the benchmark functions exist - we will introduce the new ISA instruction inside `computeACSLoop` function.
  This specific part: 
  ```
  g_acs_survivors[s] = hw_run_column(hard_symbol(EncodedStreamPtr[s]));
  ```
- bmark.c: runs Viterbi decoder on a loop for the tests 

