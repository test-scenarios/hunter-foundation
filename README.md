# Hunter Foundation

## Intention

To provide an easy way of handling cross-platform dependency management

This project will create a development environment in which your cmake
project can build. The intention of this project is to build all the
dependent libraries from source using the same toolchain as will be used
by your project.

## Requirements

The following cmake command line arguments must be set:

`FOUNDATION_PROJECT` - the path to your cmake project

The following cmake command line arguments should be set:

`CMAKE_TOOLCHAIN_FILE`

