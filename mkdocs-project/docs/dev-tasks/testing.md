# Development Tasks / Testing

Automating software testing is an important software development task because it helps ensure that software performs as intended.
It is particularly important to ensure that a change in one part of the code does not break another part of the code,
and that changes in the computer environment don't break the software.

This documentation contains the following sections:

* [Introduction](#introduction)
* [Test StateCU by Running Reference Datasets](#test-statecu-by-running-reference-datasets)
* [Automated Functional Testing Using TSTool](#automated-functional-testing-using-tstool)
* [Test Code Using Unit Tests](#test-code-using-unit-tests)

----------------

## Introduction

Automated testing of StateCU software has not been formalized into a software framework in the past.
This documentation describes the current state of testing.
The [`cdss-app-statecu-fortran-test`](https://github.com/OpenCDSS/cdss-app-statecu-fortran-test)
repository contains StateCU tests.

Testing generally involves two approaches:

1. Create small stand-alone tests that test specific software features,
such as a consumptive use method or model option,
to verify specific computational code.
These tests are not currently included in StateCU test repository but could be added,
similar to StateMod or TSTool software tests.
2. Run full datasets using different StateCU executable versions and compare the results.
This helps identify the impacts of a change in one version compared to a baseline version.
The baseline version is typically the latest published release
that it has been sufficiently tested and verified.
This approach is the focus of current automated testing.

The following sections provide more details about testing.

## Test StateCU by Running Reference Datasets

The current approach to testing StateCU is to run entire datasets using different StateCU versions
and compare the results to ensure that differences are small or are otherwise explainable.
This approach is described in the
[`cdss-app-statecu-fortran-test` `README`](https://github.com/OpenCDSS/cdss-app-statecu-fortran-test).

## Automated Functional Testing Using TSTool

TSTool software is used to implement dataset tests as described in the previous section.
TSTool can also be used to implement automated tests on small datasets and run suites of tests.
This approach can be used if small datasets are created for testing.

## Test Code Using Unit Tests

Unit tests are compiled code the test an atomic unit of code.
Unit tests are a tool for software developers that require access to the develop environment,
unlike functional tests, that could be run by users without the full developer environment.

There does not seem to be extensive unit test frameworks for Fortran.  See:

* [A look at FORTRAN unit test frameworks](https://www.software.ac.uk/blog/2016-09-28-look-fortran-unit-test-frameworks)

Unit tests could be implemented in the future,
especially if StateCU is ported to another language that provides a unit test framework.
