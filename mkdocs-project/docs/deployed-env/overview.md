# Deployed Environment / Overview

This documentation discusses how StateCU should be deployed into an operational environment.
It is important to keep this target in sight as the end result of software development.
StateCU modelers that are not developers will only be working in the deployed environment.

Software development occurs using version-controlled copies of files that
are different than the deployed environment.
See [New Developer Setup](../dev-new/overview.md) documentation for how to set up a new developer environment.
Files from the developer environment can be installed to the deployed environment for local testing.

This documentation contains the following sections:

* [Packaging the StateCU Executable with StateCU Dataset](#packaging-the-statecu-executable-with-statecu-dataset)
* [Packaging the StateCU Executable with StateCU GUI](#packaging-the-statecu-executable-with-statecu-gui)
* [StateCU 32 and 64 Bit Executable Considerations](#statecu-32-and-64-bit-executable-considerations)

-----------------

## Packaging the StateCU Executable with StateCU Dataset

Each StateCU dataset contains the `StateCU` folder for model input files.
Some CDSS datasets include the StateCU executable with input files to ensure that the correct version
of the software is used with the dataset.
This approach can avoid problems and is recommended for deployment.

As of StateCU 14.0.0, the executable is available on the
[OpenCDSS website](https://opencdss.state.co.us/statecu/) in a zip file.
A specific StateCU executable version can be packaged with a StateCU dataset by
copying the `statecu*.exe` executable file into the dataset `StateCU` folder.
The `statecu.cmd` file can also be packaged with a dataset to provide a general command
for command-line use and to call from the StateCU GUI.

## Packaging the StateCU Executable with StateCU GUI

**As of StateCU 14.0.0, the executable is available on the
[OpenCDSS website](https://opencdss.state.co.us/statecu/) in a zip file.
The executable name contains the version to uniquely identify the software version.
The StateCU executable is also distributed with a general `statecu.cmd` file
that can be used to run the most recent executable, for example from the StateCU GUI.
The StateCU GUI can be updated to use the general `statecu.cmd` program
as the default and can also rrun the version in a dataset's `StateCU` folder.**

The approach for distributing the StateCU executable (as of version 13.03) has been to package the `statecu.exe` file
with the StateCU GUI and datasets, as described in the next two sections.
For example, see the [CDSS StateCU](https://cdss.colorado.gov/software/statecu) web page.
For Windows, the software defaults to an installation folder: 

```
C:\CDSS\StateCU\bin\
    statecu.exe                             (StateCU model executable)
    statecui.exe                            (StateCU GUI executable)
    other files                             (Many other files are used by the GUI)
```

### Information from Jim Brannon about the StateCU GUI

The following information was provided during initial OpenCDSS repository configuration.

* The current StateCU GUI is VB code, rewritten only where it had to be from the original VB6.
In other words, a lot of the original VB6 code is still in there - but it compiled, so it was left alone.
It is not modern era VB.NET at all. Therefore it can't be compiled except on the LRE computer given to DWR. Kelley T or Mary H has it.

* When I started working on StateCU, we (LRE) moved both the FORTRAN and VB6 code into the Visual Studio environment and begin using Intel FORTRAN.
Later I separated the FORTRAN StateCU code from Visual Studio, and modified it to be amenable to other compilers like gfortran.
At that time at LRE, we were not using a version control system, so complete sets of StateCU code for each version were kept in carefully named folders.
StateCU FORTRAN code was finally added to a version control system (git) much later, but StateCU code was changing infrequently by that time.

## StateCU 32 and 64 Bit Executable Considerations

**As of StateCU 14.0.0, the software is distributed as a 64-bit executable.
The following information is for historical purposes only and can be used to confirm whether an executable is 32-bit or 64-bit.**

The StateCU software is a Fortran program that is compiled to a 32-bit static executable using the `gfortran` compiler.
The 32-bit Windows executable will run on 64-bit Windows 7 and 10 computers similar to other 32-bit software.
Although creating a 64-bit executable may be desirable or necessary in the future, it is currently not the focus of development,
and will require an evaluation of code memory logic and binary output file structure.
See the following resources to understand whether a program has been compiled as a 32-bit or 64-bit executable:

* [10 Ways to Determine if Application is Compiled for 32-bit or 64-bit](https://www.raymond.cc/blog/determine-application-compiled-32-64-bit/)

Based on the above, a useful utility to examine executable properties is the [7zip](http://www.7-zip.org/download.html) software.
Once installed, 7Zip can be used to examine the `statecu.exe` file as follows (the following uses an "el" not "one" 7zip command).
The `CPU = x86` indicates 32-bit, corresponding to i386 computer chips.  A 64-bit executable has `CPU = x64`.

```text
> "C:\Program Files\7-Zip\7zexe" l statecu.exe

7-Zip [64] 16.04 : Copyright (c) 1999-2016 Igor Pavlov : 2016-10-04

Scanning the drive for archives:
1 file, 4587318 bytes (4480 KiB)

Listing archive: statecu.exe

--
Path = statecu.exe
Type = PE
Physical Size = 4587318
CPU = x86
Characteristics = Executable 32-bit NoRelocs NoLineNums
Created = 2017-01-01 03:14:44
Headers Size = 1024
Checksum = 4635747
Image Size = 596111360
Section Alignment = 4096
File Alignment = 512
Code Size = 2475520
Initialized Data Size = 3134976
Uninitialized Data Size = 591632896
Linker Version = 2.25
OS Version = 4.0
Image Version = 1.0
Subsystem Version = 4.0
Subsystem = Windows CUI
Stack Reserve = 2097152
Stack Commit = 4096
Heap Reserve = 1048576
Heap Commit = 4096
Image Base = 4194304

   Date      Time    Attr         Size   Compressed  Name
   ------------------- ----- ------------ ------------  ------------------------
   2017-01-01 03:14:44 .....      2475520      2475520  .text
   2017-01-01 03:14:44 .....         2560         2560  .data
   2017-01-01 03:14:44 .....       613888       613888  .rdata
   2017-01-01 03:14:44 .....        38912        38912  /4
   2017-01-01 03:14:44 .....            0            0  .bss
   2017-01-01 03:14:44 .....         3072         3072  .idata
   2017-01-01 03:14:44 .....          512          512  .CRT
   2017-01-01 03:14:44 .....          512          512  .tls
   2017-01-01 03:14:44 .....         2048         2048  /14
   2017-01-01 03:14:44 .....       765952       765952  /29
   2017-01-01 03:14:44 .....        16896        16896  /41
   2017-01-01 03:14:44 .....       522240       522240  /55
   2017-01-01 03:14:44 .....         1536         1536  /67
   2017-01-01 03:14:44 .....         1024         1024  /78
   2017-01-01 03:14:44 .....       141622       141622  COFF_SYMBOLS
   ------------------- ----- ------------ ------------  ------------------------
   2017-01-01 03:14:44            4586294      4586294  15 files
```

Another option is to use an editor that can edit a binary file. 
For example, use Windows `Notepad`, `Notepad++`, or `vim -b` editors.
Search for the characters `PE` at the top of the file.

* If these characters are followed closely by `L`, then the executable is 32-bit.
* If these characters are followed closely by a `d`, then the executable is 64-bit.

