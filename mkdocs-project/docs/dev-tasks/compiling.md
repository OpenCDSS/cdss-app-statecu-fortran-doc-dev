# Development Tasks / Compiling

StateCU code is compiled using a "makefile", which defines rules for detecting when a file needs to be recompiled,
based on code dependencies.
The code can be compiled from command line or from the Eclipse IDE.
The Eclipse IDE provides benefits during development such as debugging and code completion
but does require more training/learning to use.

This documentation contains the following sections:

* [Compile StateCU on Command Line](#compile-statecu-on-command-line)
* [Compile StateCU in Eclipse](#compile-statecu-in-eclipse)

-----------------

## Compile StateCU on Command Line

Compiling on the command line uses the `make` command and `makefile`.

### Linux

Compiling on Linux is similar to Windows.  Use the `make` command targets.

### Windows - MinGW

To compile StateCU, open an ***MSYS2 MinGW 64-bit*** window.
There is no need for any additional configuration (as was required in earlier 32-bit StateCU development environment).

Then change to the code location and run the makefile,
replacing `user` with the appropriate user name:

```
> cd /C/Users/user/cdss-dev/StateCU/git-repos/cdss-app-statecu-fortran/src/main/fortran
> make veryclean
> make statecu_prog
```

The executable with name similar to `statecu-14.0.0-gfortran-win-64bit.exe`
is created in the same folder and can be run with model input,
such as in a test folder separate from the code.
The version will match that in the `gcommon.inc` file.

Use the `make help` command to list available `makefile` targets.
The following are the main targets that are useful during development:

| **`makefile` Target**&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | **Description** |
| -- | -- |
| `clean` | Remove dynamically created files (but not final executable). |
| `help` | Print help. |
| `installer` | Create the StateCU software installer zip file. |
| `statecu_prog` | Compile the StateCU executable, recompiling any `.o` if `.for` files are modified.  Same as `statecu_o3` to compile the optimized variant for testing.  **Use for normal development.**
| `statecu_check` | Compile the StateCU executable including all runtime checks. |
| `statecu_o3` | Compile the StateCU executable for optimization level 3 and limited runtime checks.  Use for production release and full testing. |
| `statecu_release` | Do clean compile on `check` and `o3` release variant and copy `o3` variant to plain name without `-o3` for release. **Use to prepare for software release.** |
| `veryclean` | Make the 'clean' target, and also remove the final executable. |
| `veryclean_check` | Needed by `statecu_release`. |
| `veryclean_o3` | Needed by `statecu_release`. |

A typical development session will involve repeating:

1. editing source code
2. `make statecu_prog`
3. Copy the excutable to `StateCU` folder of a dataset for testing.  See the [Testing](testing.md) documentation.

## Compile StateCU in Eclipse

**This documentation is out of date and needs to be updated.
Eclipse has not been actively used in development.**

StateCU can also be compiled using Eclipse, which relies on the `make` command and `makefile`.

### Linux

This documentation will be completed when resources are available for Linux development and testing.

### Windows - MinGW

To compile StateCU in Eclipse, start Eclipse with the run script `run-eclipse-statecu-mingw.bat` as shown below.
This script automatically runs the MinGW setup script described in the previous section,
which will configure the compiler environment if necessary.


```
> C:
> cd \Users\user\cdss-dev\StateCU\git-repos\cdss-app-statecu-fortran\build-util\eclipse
> run-eclipse-statecu-mingw.bat
```

Then right-click in the ***Project Explorer*** area and select ***Make / Targets***.  Then select ***Build...***.  Then select a target and press the ***Build*** button.

Review the output in the ***Console*** area to see if any errors occurred.
