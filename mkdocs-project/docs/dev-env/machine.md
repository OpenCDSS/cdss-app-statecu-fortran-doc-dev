# Development Environment / Machine

The computer and operating system used for development control how other software components are installed.
The target environment is Windows 10+ and Linux, with initial focus being Windows given the
needs of the State of Colorado and its contractors.

StateCU code is Fortran and there is a desire to use the free and open source `gfortran` compiler,
rather than previous Lahey and Intel compilers.
As of StateCU 14.0.0, 64-bit `gfortran` is used to compile StateCU.

**The initial approach for StateCU is to use a MinGW `gfortran` environment within Windows,
given that this approach has been implemented with success previously.
When more time is available, Cygwin and Linux development environments will also be tested and documented,
to allow more flexibility for developers that prefer or require those environments.**

The following sections are included in this documentation.
**The choice of development environment by the software developer will drive many other configuration steps.
Again, MinGW is the initial focus.**

* [Linux](#linux)
* [Windows](#windows)
	+ [Install MinGW](#install-mingw)
	+ [Install Cygwin](#install-cygwin) - future development environment option

--------------------

## Linux

This section will be completed when resources are available to focus on Linux development and testing.

## Windows

The configuration of the 64-bit `gfortran` environment is the same as StateMod.
Refer to the [StateMod Developer Documentation](https://opencdss.state.co.us/statemod/latest/doc-dev/dev-env/machine/).

An archive of old [32-bit documentation is available as a reference](machine-32bit.md)
and will be removed in the future.
This approach was used prior to using 64-bit `gfortran` as of StateCU 14.0.0.

### Install Cygwin

This section can be completed if necessary.  The Native Windows MinGW development environment is currently the focus.
Cygwin can be useful in cases where software is not available in Git Bash or Windows.
