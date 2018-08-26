## Prerequisites

```
$ sudo apt install gdb valgrind build-essential python3-minimal python-minimal
$ cd ~
$ git clone https://github.com/niklasb/gdbinit
$ cd gdbinit
$ ./setup.sh
```

Then, build AFL with qemu mode support and `afl_patches.diff` applied. Set
`AFL_PATH` correctly in your `.bashrc`.

## Setup

1. `git clone https://github.com/niklasb/bspfuzz/ && cd bspfuzz`
2. Copy over `bin/` and `csgo/` directories from the CS:GO server installation
   into the `bspfuzz` directory
3. `cp bin/dedicated.{,orig.}so && cp bin/engine.{,orig.}so && cp bin/libtier0.{,orig.}so`
4. Adapt offsets in `main.cpp` and `patch.py` for your version
5. `make && make patch`
6. `mkdir -p fuzz/{in,out} && cp mini_bsp/test_mini.bsp fuzz/in`

## Running

```
$ cd /path/to/bspfuzz
$ ./run_afl.sh 1
$ ./run_afl.sh 2
$ ./run_afl.sh 3
...
```

## Triaging

```
cd /path/to/bspfuzz/triage
./triage.sh
./valgrind.sh
```
