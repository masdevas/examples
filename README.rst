********************************
Example applications for Gramine
********************************

.. This is not |~|, because that is in rst_prolog in conf.py, which GitHub cannot parse.
   GitHub doesn't appear to use it correctly anyway...
.. |nbsp| unicode:: 0xa0
   :trim:

.. highlight:: sh


This repository contains a curated set of Gramine examples. These examples are
tested only against stable Gramine releases (i.e., these examples are not
guaranteed to work with non-release versions of Gramine, including the latest
master-branch commits of Gramine). The examples were tested on Ubuntu 18.04 and
20.04.

For instructions how to build and run each application under Gramine, please
see the README in each subdirectory.

Please note that most of the examples use oversimplified configurations which
are *not secure*. E.g., we frequently specify security-critical files as
``sgx.allowed_files``. If you take these examples as templates for your own
production workloads, please inspect and harden the configurations.

We recommend to look at the (extensively commented) `Redis example
<https://github.com/gramineproject/gramine/tree/master/CI-Examples/redis>`__
to get an idea how to write the README, Makefile and manifest files. If you want
to contribute a new example to Gramine and you take the Redis example as a
template, we recommend to remove the comments from your copies as they only add
noise (see e.g. Memcached for a "stripped-down" example).

Known unsupported applications
==============================

Some applications are known to *not* run in Gramine. Typically this is because
these applications depend on features currently not implemented in Gramine.

We are aware of the following unsupported applications:

- Apache web server: depends on Sys-V semaphores, unimplemented in Gramine.


Building examples
=================

All our examples use simple Makefiles to build the original application (if
needed) and configure it to run in Gramine. Use one of these commands:

- ``make``: create non-SGX no-debug-log manifest
- ``make DEBUG=1``: create non-SGX debug-log manifest
- ``make SGX=1``: create SGX no-debug-log manifest
- ``make SGX=1 DEBUG=1``: create SGX debug-log manifest

Use ``make clean`` to remove Gramine-generated artifacts and ``make distclean``
to remove all build artifacts (if applicable).

How to Contribute?
==================

Please put your application sample in a subdirectory with a comprehensible name.
Ideally, the subdirectory name should be the same as your application. In
addition, your application sample should have the following elements:

- ``README.md``:
  Please document the tested environment and instructions for building and
  running the application. If your application sample has any known issues or
  requirements, please also specify them in the documentation.

- ``Makefile``:
  Users should be able to build your application sample by running the ``make``
  command. If your application needs extra building steps, please document them
  in the ``README.md``. If your application also runs on Intel SGX, please
  include the commands for signing and retrieving the SGX token in the
  ``Makefile``.

- Manifest:
  Please provide the manifest needed for running your application sample. Do not
  hard-code any user-specific path or personal info in the manifest. The ideal
  way is to create a manifest template that contains variables to be replaced by
  runtime options in ``Makefile``. See other subdirectories for examples of the
  manifest templates.

- Sample inputs and test suites:
  If you have any inputs and test suites for testing the application,
  please provide them in the same subdirectory, too.

Please do not include any tarball of source code or binaries in the application
samples. If an application requires downloading the source code or binaries,
please provide instructions in the ``README.md``, or download them automatically
and verify the checksums as part of the build process.
