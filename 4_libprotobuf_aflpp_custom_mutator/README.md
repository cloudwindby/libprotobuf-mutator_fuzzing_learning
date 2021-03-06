# Combine libprotobuf-mutator with AFL++

* `lpm_aflpp_custom_mutator.cc`: Shared library for AFL++  
    - Custom mutate `TEST` protobuf
    - Convert the protobuf to raw data
* `lpm_aflpp_custom_mutator.h`: Declare `afl_custom_mutator` as a friend function so it can use protobuf's mutators  
* `vuln.c`: Vulnerable C program  

## Makefile

* Modify `PROTOBUF_DIR` to your own protobuf installation path  
* Modify `LPM_DIR` to the root direcotry of libprotobuf-mutator  
* Modify `AFLCC` to the path of an AFL++'s compiler  


## Test the program  
* `make`
    - This will create `lpm_aflpp_custom_mutator.so`, the shared library for AFL++ ( for custom mutator's usage )  
* `make vuln` to create the vulnerable binary  
* `run_fuzz.sh`  
    - Modify the path of `afl-fuzz` before you run the script
* It should generate the crash samples immediately  
    * Check `out/crashes/id000xxxxx.........`  
    * The first byte of the crash sample should be `0xe8` or `0x02`
