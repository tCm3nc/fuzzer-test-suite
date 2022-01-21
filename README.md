# fuzzer-test-suite

:zap: **NOTE: For most use cases, fuzzer-test-suite is superseded by [FuzzBench](https://github.com/google/fuzzbench). 
We recommend using FuzzBench for all future fuzzer benchmarking. 
FuzzBench is based on many of the same ideas as FTS, such as realistic benchmarks (it actually uses some benchmarks from FTS) but has many improvements such as a free service and a design that makes adding new fuzzers and new benchmarks easier.**

This is a set of tests (benchmarks) for fuzzing engines (fuzzers).

The goal of this project is to have a set of fuzzing benchmarks derived from real-life
libraries that have interesting bugs, hard-to-find code paths, or other
challenges for bug finding tools.

The current version supports [libFuzzer](http://libFuzzer.info) and
[AFL](http://lcamtuf.coredump.cx/afl/).  In future versions we may support
other fuzzing engines.

# Usage

To compile a project defined in this suite try the following example:

```bash
cd ~
git clone https://github.com/google/fuzzer-test-suite
cd ~
git clone https://github.com/AFLplusplus/AFLplusplus
mkdir clean_aflplusplus
mv aflplusplus clean_aflplusplus
cd clean_aflplusplus/aflplusplus
make && make llvm
cd ~
mkdir benchmark
cd benchmark
AFL_SRC=~/clean_aflplusplus/aflplusplus FUZZING_ENGINE=afl ~/fuzzer-test-suite/build-and-test.sh c-ares-CVE-2016-5180
# In a separate terminal:
cd clean_aflplusplus/aflplusplus
mkdir input output
echo "z" > input/z
./afl-fuzz -i input -o output -- ~/benchmark/RUNDIR-c-ares-CVE-2016-5180/c-ares-CVE-2016-5180-afl
```

# See also

* [AddressSanitizer](http://clang.llvm.org/docs/AddressSanitizer.html)

# Contributing
See [CONTRIBUTING](CONTRIBUTING) first. 
If you want to add one more benchmark to the test suite,
simply mimic one of the existing benchmarks and send the pull request. 

# Disclaimer
This is not an official Google product.
