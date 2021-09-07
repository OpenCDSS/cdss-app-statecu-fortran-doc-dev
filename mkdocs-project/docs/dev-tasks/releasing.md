# Development Tasks / Releasing

Releasing the software consists of compiling StateCU into an executable and packaging into an installer that can be distributed.
The StateCU executable may be further packaged with StateCU datasets and StateCU GUI,
although this documentation does not currently describe those steps.

This documentation contains the following sections:

* [Build and Release Checklist](#build-and-release-checklist)
* [Creating StateCU Installer](#creating-statecu-installer)
* [Releasing StateCU](#releasing-statecu)

--------------------

## Build and Release Checklist

Currently there is not a need for StateCU to be built in a continuous integration process because the development team is small
and software development is infrequent, rather than continuous.
Consequently the build and release process is done by the primary developer(s).

The full build process checklist is as follows.
All release artifacts include the version found in the software code.

1. As of version 14.0.0, the software version has 3 parts such as 14.0.0.
The version should be incremented accordingly as public releases are made
based on [Semantic versioning](https://semver.org/).
If necessary, add a fourth part such as `.dev1`, `.dev2`, etc. to indicate development versions that
are not intended for public use.
2. Issues in the GitHub repository should be coordinated to decide when a public versioned release should occur.
Normally a release will be made to fix bugs only and/or to introduce one or more new features.
3. Recompile the program for release in `src/main/fortran` folder:  `make statecu_release`
4. Run tests to confirm program accuracy. See the [Testing](testing.md) documentation.
5. Update the documentation, in particular user documentation and release notes.  See the [Documenting](documenting.md) documentation.
6. Create the installer.
The [Creating StateCU Installer](#creating-statecu-installer) section below discusses the installer in more detail.
7. Publish the new version.  The compiled executable can be distributed.  See the [Releasing StateCU](#releasing-statecu) section below.

## Creating StateCU Installer ##

StateCU software executables are packaged into a zip file by running the following `make` target in the
`src/main/fortran` folder:

```
make installer
```

This runs the `build-util/copy-to-co-dnr-gcp.bash` script,
which creates the zip file, optionally uploads to the OpenCDSS Google Cloud Platform bucket/website,
and optionally creates an updated
[StateCU index page](https://opencdss.state.co.us/statecu/).

## Releasing StateCU

The previous section describes how to create and upload a zip file installer for the StateCU executables.
The executables can be packaged into other products as described in the
[Deployed Environment / Overview](../deployed-env/overview.md) documentation.

Old comments from Jim Brannon:

* Long ago memory here, but I am pretty sure the latest (and only) StateCU install packages that CDSS distributes
came from me creating a setup package using the OLD Visual Studio on that OLD laptop that DWR has.
Very dated stuff. For Willem for RGDSS, I just sent him the open source version of the source code.
He didn't want the GUI.  There were some special features we (LRE) added just for RGDSS and he may have added some more himself.
