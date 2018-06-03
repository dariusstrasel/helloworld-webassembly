# helloworld-webassembly

Made posibble by: https://webassembly.org/getting-started/developers-guide/

Summary:
This project contains the output from the getting started guide in the above link. I had to setup my environment for this, and so I will document the pre-reqs in addition to compilation steps.

General Pre-Reqs:
Git, CMake, Host system compiler, python

Tool Chain Pre-Requisites:
- (cmake)[https://cmake.org/download/]
-- If using windows, you can install this via chocolately:
```powershell
choco install cmake
```
- (emscriptem-sdk)[https://github.com/juj/emsdk]

## Installing the tool chain (Using c/c++)
```bash
git clone https://github.com/juj/emsdk.git
cd emsdk
./emsdk install latest
./emsdk activate latest
```
Entering the compiler environment:

```bash
source ./emsdk_env.sh --build=Release
```

## Compiling a webassembly program:
```bash
mkdir hello
cd hello

touch hello.c
```

Use your preferred text editor to enter the following:
```c
#include <stdio.h>
int main(int argc, char ** argv) {
  printf("Hello, world!\n");
}
```

To compile into webassebly, run the following:
```bash
emcc hello.c -s WASM=1 -o hello.html
```

emcc: emscriptem compiler executable  
hello.c: Your c or c++ source file  
-s WASM=1: linker flag which tells emcc to produce wasm instead of asm.js  
-o hello.html: flag which tells emcc to produce an html file in addition to the necessary files  

To verify your output, run a webserver in the current directory. emcc provides a command for us:
```bash
emrun --no_browser --port 8080 .
```
