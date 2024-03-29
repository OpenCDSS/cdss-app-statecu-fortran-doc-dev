# Development Environment / Machine (32-bit Windows `gfortran`)

**This documentation is being retained as an archive.
However, the current development enviroment as of StateCU 14.0.0 uses 64-bit machine as
described in the current [Development Environment / Machine](machine.md) documentation.**

## Introduction

The use of `gfortran` somewhat constrains the development environment, especially on Windows,
requiring that either MinGW or Cygwin are used for development,
each of which mimic Linux functionality but will result in Windows-compatible binary StateCU executable.
Using Eclipse/Photran IDE provides some isolation from the command line environment,
but developers will be more effective if they understand command line programs
and some developers may choose to use text editor and command line tools.

MinGW or Cygwin are the recommended compiler environments.
MinGW will be the focus as it has been previously used to compile StateCU.

## Windows ##

The following is the old machine setup documentation for 32-bit `gfortran` environment.

### Install MinGW - Native Windows 32-bit

This documentation needs to be updated to use newer versions of MINGW.
There seem to be newer versions of gcc/gfortran available but the MinGW documentation is somewhat old, 2013?.
Installing the MinGW as shown below seems to install recent compilers.

The Minimalist GNU for Windows (MinGW) environment provides a minimal Linux implementation on Windows.
MinGW provides an environment in which the `gcc` and `gfortran` compilers will run.

Note that various software tools are shipped to run inside a MinGW environment, including Git for Windows,
separate from the MinGW implementation that is used to compile code.
It is OK to have multiple MinGW environments installed, as long as the software developer understands why each was installed
and does not get confused.  For example, if a Bash shell is used, the title bar usually indicates what environment is being used.
See the following installation instructions:

* [MinGW Getting Started](http://www.mingw.org/wiki/Getting_Started)

If MinGW has previously been installed, it does not need to be reinstalled.
Look for a `C:\MinGW` folder.  If it exists, then MinGW was previously installed and can be used for StateCU development.

If MinGW needs to be installed, then as recommended in the MinGW Getting Started documentation, use the Graphical User Interface Installer.
First retrieve the [`mingw-get-setup.exe`](https://sourceforge.net/projects/mingw/files/latest/download) program (click on the link),
which will save to the `Downloads` folder.

Run the downloaded `mingw-get-setup.exe` program and follow the steps below.

![install MinGW 1](machine-images/install-mingw-1.png)

Press ***Install***

![install MinGW 2](machine-images/install-mingw-2.png)

The installation documentation recommends installing only for the single user (not all users).
And, because MinGW has not been updated in several years, there is little reason to change the install folder from the default.
Therefore, accept the defaults shown above by pressing ***Continue***.  Progress will be indicated as shown below:

![install MinGW 3](machine-images/install-mingw-3.png)

![install MinGW 4](machine-images/install-mingw-4.png)

At this point MinGW has been installed but the compilers have not been installed.
The following window is displayed to allow selection of additional software to install:

![install MinGW 5](machine-images/install-mingw-5.png)

StateCU requires Fortran, but select C and C++ because they may be needed for various CDSS tools.
Click on the box next to the component and select ***Mark for Installation***.

![install MinGW 6](machine-images/install-mingw-6.png)

Then use the ***Installation / Apply Changes*** menu, which will display the following:

![install MinGW 7](machine-images/install-mingw-7.png)

Press ***Apply*** to commit the selections.  The following progress dialogs will be shown.

![install MinGW 8](machine-images/install-mingw-8.png)

![install MinGW 9](machine-images/install-mingw-9.png)

Press ***Close***.  The successfully installed packages will be indicated as shown below.
The following indicates that `gcc` and `gfortran` version 5.3.0-3 were installed.
See below for confirmation of the version.

![install MinGW 10](machine-images/install-mingw-10.png)

**This documentation needs to be updated to describe the implications of 32-bit and 64-bit.
StateCU has traditionally been compiled as a 32-bit application,
which seems consistent with the MinGW install, but need to understand how 64-bit MinGW can
be used and whether both 32-bit and 64-bit can be installed on the same computer.**

The MinGW files should have been installed in `C:\MinGW` and can be confirmed by inspection.

#### Configure MSys

As per the installation instructions, confirm that the file `C:\MinGW\msys\1.0\etc\fstab` correctly indicates where MinGW is installed.
The following was the default and appears to be correct.

```text
# /etc/fstab -- mount table configuration for MSYS.
# Please refer to /etc/fstab.sample for explanatory annotation.

# MSYS-Portable needs this "magic" comment:
# MSYSROOT=C:/MinGW/msys/1.0

# Win32_Path                            Mount_Point
#-------------------------------------  -----------
C:/MinGW                                /mingw

```

#### Configure `PATH`

As per the installation instructions, in order for the operating system to find the programs,
the `PATH` environment variable needs to be updated.
The installation instructions recommend setting with a script.
Therefore, create a script `setup-mingw-env.bat`, with contents similar to the following:

```bat
rem Setup the MinGW environment variables
rem See:  http://www.mingw.org/wiki/Getting_Started

rem Update PATH to find the MinGW bin folder and also the MSYS folders (Unix utilities).
set PATH=C:\MinGW\bin;C:\MinGW\MSYS\1.0\local\bin;C:\MinGW\MSYS\1.0\bin;%PATH%
```
This script is included in the repository in a `build-util/mingw` folder for use by developers.
It is also called by the `eclipse/run-eclipse-statecu-mingw.bat` batch file to facilitate running Eclipse with the correct environment.

#### Confirm Compiler Version

Once the `PATH` has been configured as described in the previous section (by running the `setup-mingw-env.bat` batch file),
the compiler versions can be confirmed, as followed,
from a Windows command shell.  Or, alternatively, start a Windows command shell and then run `bash` to start a Linux Bash shell.
Both will allow running the following commands.

```com
> gcc --version
gcc (GCC) 5.3.0
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

> gfortran --versionGNU Fortran (GCC) 5.3.0
Copyright (C) 2015 Free Software Foundation, Inc.

GNU Fortran comes with NO WARRANTY, to the extent permitted by law.
You may redistribute copies of GNU Fortran
under the terms of the GNU General Public License.
For more information about these matters, see the file named COPYING
```
