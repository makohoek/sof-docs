.. _cmake:

CMake Arguments
###############

Firmware & Unit Tests
*********************

TOOLCHAIN
   Specifies toolchain to use, usually it's prefix to tools that
   follow GCC naming convention. Toolchain should contain tools like:

   * <prefix>-gcc
   * <prefix>-ar
   * <prefix>-objdump
   * <prefix>-objcopy

   There are more tools from GCC-like toolchains that may be used by build
   system, but these are used in most cases.
   For example toolchain *xtensa-apl-elf*, should have tools xtensa-apl-elf-gcc,
   xtensa-apl-elf-ar, etc.
   Toolchain has to be in PATH.

   .. code-block:: bash

      # Examples
      cmake [...] -DTOOLCHAIN=xt [...]
      cmake [...] -DTOOLCHAIN=xtensa-apl-elf [...]
      cmake [...] -DTOOLCHAIN=xtensa-cnl-elf [...]

ROOT_DIR
   Path to directory with xtensa core's lib and include.

   .. code-block:: bash

      # Examples
      cmake [...] -DROOT_DIR=$CONFIG_PATH/xtensa-elf [...]
      cmake [...] -DROOT_DIR=/my-xtensa-newlib/xtensa-root/xtensa-apl-elf [...]

MEU_PATH
   Path to directory with MEU tool. For example full path to MEU that will
   be used, should be `$MEU_PATH/meu` or `$MEU_PATH/meu.exe`. 

   .. code-block:: bash

      # Example
      cmake [...] -DMEU_PATH=/path/to/meu/installation [...]

MEU_PRIVATE_KEY
   Path to file with key that will be used by meu.

   .. code-block:: bash

      # Example
      cmake [...] -DMEU_PRIVATE_KEY=/path/to/meu/private-key.pem [...]

Unit Tests
**********

BUILD_UNIT_TESTS
   Default: OFF, if ON then builds unit tests.

   .. code-block:: bash

      # Example: build unit tests instead of firmware
      cmake -DTOOLCHAIN=xt -DROOT_DIR=$CONFIG_PATH/xtensa-elf -DBUILD_UNIT_TESTS=ON [...]

CMOCKA_DIRECTORY
   Path to directory with prebuilt Cmocka library.
   Usually you shouldn't use it, because if this argument is not used, then
   CMake will build Cmocka automatically for you in build directory.
   Cmocka directory should contain include subdirectory with `cmocka.h` header
   and lib subdirectory with `cmocka-static.a` library.

   .. code-block:: bash

      # Example
      cmake [...] -DCMOCKA_DIRECTORY=/path/to/cmocka-install-apl [...]

Host Testbench
**************

BUILD_HOST
   Default: OFF, if ON then builds testbench for host.
   
   .. code-block:: bash

      # Example: build testbench instead of firmware
      cmake -DBUILD_HOST=ON -DCMAKE_INSTALL_PREFIX=install [...]
