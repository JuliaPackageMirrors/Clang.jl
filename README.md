CINDEX.jl provides a wrapping of libclang for the 
Julia language (http://julialang.org)

libclang provides access to the C/C++ AST generated by the 
parser from the LLVM Clang project.

## Status

Preliminary. Most CXCursor and CXType related functions are
wrapped, providing AST browsing and printing functionality.
See examples/print_functions.jl and examples/README

All testing and development so far has been on Ubuntu 12.04.1 (64-bit)

## Prerequisites

libclang must be available as a shared library. libclang can
optionally be built by the Julia build system by setting 
BUILD_LLVM_CLANG=1 in julia/deps/Makefile.

## Implementation

Most libclang functions pass and return small 
structs by value. As Julia does not (yet) have full struct 
support, the current CINDEX.jl implementation includes a 
C++ wrapper. clang functions are wrapped by a C++ function
that memcpys data to/from a Julia-owned memory array 
(passed by pointer)

see cindex_base.jl and wrapcindex.h for generated wrappers.

Some functions are manually wrapped for convenience and ease of
implementation, or to provide a more Julia-friendly API.

see cindex.jl and wrapcindex.cpp

### License

CINDEX.jl is licensed under the MIT license.
