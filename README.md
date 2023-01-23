top level note:
Visual Studio builds are broken

## ( **libOHFUCK** )
convenience library for the OHFUCK project

you can use it in your own project too, just read this file carefully
- no external dependencies
- useful macros and object programming in C99
- simple `CMAKE` package exported as a static or shared library
  - works on `UNIX-like` systems 
  - probably works on `microsoft™ windows™`

### ( **building** )

you can build `libOHFUCK` as a shared or static library.
the static library route is chosen by default

**requirements**:
- the almighty `CMAKE` version 3.4 or greater
- C99 compatible compiler
  - `CLANG` or `GCC` are recommended [^1]

by default:
- a static library will be built (build a shared one with `-DBUILD_SHARED_LIBS=1`
- `libOHFUCK` will be placed under `C:\Program Files (x86)`, `/usr/local`
or wherever `CMAKE` feels like putting it

**step by step**:

in a terminal, CD into the `libohfuck` folder
  > use `cmake` with the `-G` flag to specify a compiler toolchain, e.g.
    `cmake .. -G 'Unix Makefiles'`
  
  > on Windows you might need to run `cmake --install` with elevated privileges so that
  it can write to `Program Files (x86)`
  - `UNIX-like` systems, `microsoft™ windows™` with `MinGW`:

        $ mkdir build ; cd build
        $ cmake .. -DCMAKE_BUILD_TYPE=Release
        $ cmake --build . ; cmake --install .
        $ # if 'cmake --install .' fails, try running with 'sudo'

  - `microsoft™ windows™` with `Visual Studio Tools`:

        > mkdir build ; cd build
        > # replace 'Visual Studio 17 2022' with your version 
        > cmake .. -G 'Visual Studio 17 2022'
        > cmake --build . --config Release
        > cmake --install .
  if everything went as planned, you can go to the **usage** section

### ( **usage** )
TODO

### ( **folder structure** )

    - include                 public project headers
    - src                     project source files
    - CMakeLists.txt          basic configuration file for CMAKE
    - Config.cmake.in         magic goblin wizardry (necessary? to generate *.cmake config files)

[^1]: or `MSVC`