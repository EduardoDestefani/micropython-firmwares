# micropython-firmwares
Repository of personalized firmware.

## Installation of Firmwares in ESP32 boards
To know how to install the repository firmware, just install esptool module:

`pip install esptool`

Then, with the MCU connected to the computer, format the flash memory and install the firmware by following the commands (commands must be run in the same directory where the firmware is):

```python
(base) erosvatis@nucleon-Inspiron-3583:~/firmwares$ esptool.py --port /dev/ttyUSB0 erase_flash
...
Chip erase completed successfully in 10.0s
Hard resetting via RTS pin...
(base) erosvatis@nucleon-Inspiron-3583:~/firmwares$ esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash -z 0x1000 firmware.bin 
...
Wrote 1478416 bytes (998606 compressed) at 0x00001000 in 88.1 seconds (effective 134.3 kbit/s)...
Hash of data verified.

Leaving...
Hard resetting via RTS pin...
```
### Firmwares for ESP32 boards
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20ESP32%204MB). ESP32 (LOLIN32 and LOLIN32 Pro) has hardware support only for FP32/SP, are they:

- `esp32-generic_sp_v1.18-127-gf46a7140f-ulab_v5.0.1-2D-20220401.bin`; firmware with *simple* precision native, **Micropython v1.18** and **ulab v5.0.1-2d**.
- `esp32-generic_dp_v1.18-127-gf46a7140f-ulab_v5.0.1-2D-20220401.bin`; firmware with *double* precision native, **Micropython v1.18** and **ulab v5.0.1-2d**.

For SPIRAM ESP32 boards, available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20ESP32%20SPIRAM):
- `esp32-spiram_sp_v1.18-127-gf46a7140f-ulab_v5.0.1-2D-20220401.bin`; firmware with *simple* precision native, **Micropython v1.18** and **ulab v5.0.1-2d**.
- `esp32-spiram_dp_v1.18-127-gf46a7140f-ulab_v5.0.1-2D-20220401.bin`; firmware with *double* precision native, **Micropython v1.18** and **ulab v5.0.1-2d**.

Without ulab (genric and spiram), same link of ulab firmwares above:
- `esp32-generic_dp_v1.17-39-g4ada56d4c-20211022.bin`;firmware with *double* precision native, **Micropython v1.17**.
- `esp32-spiram_dp_v1.17-39-g4ada56d4c-20211022.bin`; firmware with *double* precision native, **Micropython v1.17**.
- `esp32-generic_dp_v1.18-127-gf46a7140f-20220310.bin`; firmware with *double* precision native, **Micropython v1.18**.
- `esp32-spiram_dp_v1.18-127-gf46a7140f-20220310.bin`; firmware with *double* precision native, **Micropython v1.18**.

## 1. Construction of the ulab firmwares for ESP32 boards
In Debian and derivatives the gcc-arm is very old (5.x) in the official repository. So manually install GCC-ARM current, follow ["Getting Started STM"](https://github.com/micropython/micropython/wiki/Getting-Started-STM). The chosen version was the [gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads).

Add to the end of the file .bashrc (execute `sudo nano ~/.bashrc`):

`export PATH="${PATH}:${HOME}/stm/gcc-arm-none-eabi-9-2020-q2-update/bin"`

Other dependencies are required, it is recommended to install one by one, and then perform a `sudo apt-get update`. Then, run:

```
sudo apt-get install git
sudo apt-get install build-essential 
sudo apt-get install libreadline-dev 
sudo apt-get install libffi-dev 
sudo apt-get install pkg-config
```
After installing the above dependencies. The file below will run all steps for creating the ESP32 + ULAB firmware. To do this, simply create a file with .sh extension and paste the contents below (name the file as "esp32-cmake.sh"):

```
#!/bin/bash

export BUILD_DIR=$(pwd)

echo "--- CLONING ULAB ---"
git clone --depth 1 https://github.com/v923z/micropython-ulab.git ulab

echo "--- CLONING MICROPYTHON ---"
git clone --depth 1 https://github.com/micropython/micropython.git

echo "--- CLONING ESP-IDF ---"
cd $BUILD_DIR/micropython/
git clone --depth 1 -b v4.0.2 --recursive https://github.com/espressif/esp-idf.git

echo "--- INSTALL ESP-IDF ---"
cd $BUILD_DIR/micropython/esp-idf
./install.sh
. ./export.sh

echo "--- MPY-CROSS ---"
cd $BUILD_DIR/micropython/mpy-cross
make

echo "--- ESP32 SUBMODULES ---"
cd $BUILD_DIR/micropython/ports/esp32
make submodules

echo "--- PATCH MAKEFILE ---"
cp $BUILD_DIR/micropython/ports/esp32/Makefile $BUILD_DIR/micropython/ports/esp32/MakefileOld
echo "BOARD = GENERIC" > $BUILD_DIR/micropython/ports/esp32/Makefile
echo "USER_C_MODULES = \$(BUILD_DIR)/ulab/code/micropython.cmake" >> $BUILD_DIR/micropython/ports/esp32/Makefile
cat $BUILD_DIR/micropython/ports/esp32/MakefileOld >> $BUILD_DIR/micropython/ports/esp32/Makefile

echo "--- MAKE ---"
make
```
The file with the above instructions was created by the founder of ulab, see [link](https://github.com/v923z/micropython-ulab/blob/master/build/esp32-cmake.sh). After you create the file, simply run it in the terminal:

`. ./esp32-cmake.sh`

To create firmwares of other versions for ESP32, as **SPIRAM**, just replace rows 28 to 35 of the `esp32-cmake.sh` file by:

```
echo "--- PATCH MAKEFILE ---"
cp $BUILD_DIR/micropython/ports/esp32/Makefile $BUILD_DIR/micropython/ports/esp32/MakefileOld
echo "BOARD = GENERIC_SPIRAM" > $BUILD_DIR/micropython/ports/esp32/Makefile
echo "USER_C_MODULES = \$(BUILD_DIR)/ulab/code/micropython.cmake" >> $BUILD_DIR/micropython/ports/esp32/Makefile
cat $BUILD_DIR/micropython/ports/esp32/MakefileOld >> $BUILD_DIR/micropython/ports/esp32/Makefile

echo "--- MAKE ---"
make BOARD=GENERIC_SPIRAM
```
After saving the file, run the `. ./esp32-cmake.sh` command in the terminal.

After a few minutes, the firmware is created. It is located in the `micropython/ports/esp32/build-BOARD_NAME`. Make sure that the `/build-BOARD_NAME` directory has been created successfully. Inside `/build-BOARD_NAME` Look for **firmware.bin**, this is the firmware file that should be used to install on ESP32. 

The BOARD_NAME can be:
- `GENERIC`
- `GENERIC_SPIRAM`
- `GENERIC_S2` 
- etc ... (Look at the names of the existing folders in `/micropython/ports/esp32/boards`)

#### 1.1. Creating firmware for ESP32 with FP64 configuration
To compile double precision (FP64) you need to change the file `micropython/ports/esp32/mpconfigport.h` **line 53**, from:

`#define MICROPY_FLOAT_IMPL (MICROPY_FLOAT_IMPL_FLOAT)` to `#define MICROPY_FLOAT_IMPL (MICROPY_FLOAT_IMPL_DOUBLE)`

After editing the file, perform procedures in 1 (run the `. ./esp32-cmake.sh` command in the terminal).

## Installation of Firmwares in Pyboard D-Series
To know how to install the repository firmware, just run such commands with pyboard-d in "DFU" mode. The command below must be executed in the same directory where the pydfu.py and 'firmware.dfu' files are:

`sudo python3 pydfu.py -u firmware_name.dfu`

### Firmwares STM32 for Pyboards-D SF2 boards
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF2). Pyboard-D SF2 has hardware support only for FP32/SP, are they:

- `pybd-sf2_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware with *simple* precision native, **Micropython v1.15** and **ulab v2.8.3-2D**.
- `pybd-sf2_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware with *double* precision native, **Micropython v1.15** and **ulab v2.8.3-2D**.
- `pybd-sf2_sp_v1.16-39-g4ada56d4c-ulab_v3.1.1-2d-20210703.dfu`; firmware with *simple* precision native, **Micropython v1.16** and **ulab v3.1.1-2D**.
- `pybd-sf2_dp_v1.16-39-g4ada56d4c-ulab_v3.1.1-2d-20210703.dfu`; firmware with *double* precision native, **Micropython v1.16** and **ulab v3.1.1-2D**.
- `pybd-sf2_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2d-20210918.dfu`; firmware with *simple* precision native, **Micropython v1.17** and **ulab v3.3.4-2D**.
- `pybd-sf2_dp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2d-20210918.dfu`; firmware with *double* precision native, **Micropython v1.17** and **ulab v3.3.4-2D**.
- `pybd-sf2_sp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *simple* precision native, **Micropython v1.18** and **ulab v5.0.1-2d**.
- `pybd-sf2_dp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *double* precision native, **Micropython v1.18** and **ulab v5.0.1-2d**.

Without ulab:
- `pybd-sf2_dp_v1.12-665-g60f5b941e_2020-08-22.dfu`; firmware with *double* precision native, **Micropython v1.12**.
- `pybd-sf2_sp_144mhz_v1.12-665-G60F5B941E_2020-08-22.dfu`; firmware with simple precision (SP) and 144MHz default clock, **Micropython v1.12**.
- `pybd-SF2_SP_thread_V1.12-657-G37E1B5C89_2020-08-22.dfu`; firmware allowing multithreading with simple precision (SP), **Micropython v1.12**.
- `pybd-SF2_SP_V1.12-665-G60F5B941E_2020-08-22.dfu`; firmware with *simple* precision native, **Micropython v1.12**.

### Firmwares STM32 for Pyboard-D SF3 boards
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF3). Pyboard-D SF3 has hardware support only for FP32/SP, are they:

- `pybd-sf3_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware with *simple* precision native, **MicroPython v1.15** and **ulab v2.8.3-2D**.
- `pybd-sf3_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware with *double* precision native, **MicroPython v1.15** and **ulab v2.8.3-2D**.
- `pybd-sf3_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware with *simple* precision native, **MicroPython v1.17** and **ulab v3.3.4-2D**.
- `pybd-sf3_sp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *simple* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.
- `pybd-sf3_dp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *double* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.

### Firmwares STM32 for Pyboard-D SF6 boards
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF6). Pyboard-D SF6 has hardware support for FP32/SP and FP64/DP, are they:

- `pybd-sf6_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware with *simple* precision native, **MicroPython v1.15** and **ulab v2.8.3-2D**.
- `pybd-sf6_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware with *double* precision native, **MicroPython v1.15** and **ulab v2.8.3-2D**.
- `pybd-sf6_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware with *simple* precision native, **MicroPython v1.17** and **ulab v3.3.4-2D**.
- `pybd-sf6_dp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware with *double* precision native, **MicroPython v1.17** and **ulab v3.3.4-2D**.
- `pybd-sf6_sp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *simple* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.
- `pybd-sf6_dp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *double* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.

### Firmwares STM32 for Pyboard v1.1 boards
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard%20v1.1). Pyboard v1.1 has hardware support only for FP32/SP, are they:

- `pyb-v1.1_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware with *simple* precision native, **MicroPython v1.17** and **ulab v3.3.4-2D**.
- `pyb-v1.1_dp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware with *double* precision native, **MicroPython v1.17** and **ulab v3.3.4-2D**.
- `pyb-v1.1_sp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *simple* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.
- `pyb-v1.1_dp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *double* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.

### Firmwares STM32 for Pyboard v1.0 boards
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard%20v1.0). Pyboard v1.0 has hardware support only for FP32/SP, are they:


- `pyb-v1.0_sp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *simple* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.
- `pyb-v1.0_dp_v1.18-99-g203ec8ca7-ulab_v5.0.1-2D-20220205.dfu`; firmware with *double* precision native, **MicroPython v1.18** and **ulab v5.0.1-2D**.

### Firmwares nRF for BBC Micro:bit
Firmwares available [here](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20BBC%20Microbit). BBC Micro:bit has hardware support only for FP32/SP, are they:

- `microbit_v1.12-665-g60f5b941e_2020-08-22.hex`; **MicroPython v1.12** and **ulab edited**. It is a firmware with ancient and edited ULAB, we have a few functions of the ulab source code. This is due to the little storage space of the BBC Micro:bit to contain the ulab.

The `firmware.hex` files (.bin, .elf) are generated in `micropython/ports/nrf/build-microbit/`. Take the '.hex' file and drag to pseudo pendrive "MICROBIT".

## Construction of the ulab firmwares for pyboard boards
In Debian and derivatives the gcc-arm is very old (5.x) in the official repository. So manually install GCC-ARM current, follow ["Getting Started STM"](https://github.com/micropython/micropython/wiki/Getting-Started-STM). The chosen version was the [gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads).

Add to the end of the file .bashrc (execute `sudo nano ~/.bashrc`):

`export PATH="${PATH}:${HOME}/stm/gcc-arm-none-eabi-9-2020-q2-update/bin"`

Other dependencies are required, it is recommended to install one by one, and then perform a `sudo apt-get update`. Then, run:

```
sudo apt-get install git
sudo apt-get install build-essential 
sudo apt-get install libreadline-dev 
sudo apt-get install libffi-dev 
sudo apt-get install pkg-config
```
Compiling MicroPython Mainline for [Unix/Linux](https://github.com/micropython/micropython/wiki/Getting-Started):

* With git and gcc compiler installed, choose a directory and run the commands:

```
$ git clone --recurse-submodules https://github.com/micropython/micropython
$ cd micropython
$ git submodule update --init
$ cd mpy-cross && make clean && make -j8
$ ./mpy-cross --version
$ cd ../ports/unix && make clean && make -j8 submodules && make -j8
$ ./micropython
     MicroPython v1.12-649-g27767aafa on 2020-08-10; linux version
     Use Ctrl-D to exit, Ctrl-E for paste mode
     >>>
```

### 1. Compiling micropython/ports/stm32 (for pyboard boards, etc.)
We chose [Pyboard-D SF2 board](https://store.micropython.org/product/PYBD-SF2-W4F2), defined in `micropython/ports/stm32/boards/PYBD_SF2`, such that `BOARD=PYBD_SF2`.
But there are other official micropython boards such as Pyboard V1.1 (PYBV11), Pyboard Lite v1.0 (PYBLITEV10), Pyboard-D SF3 (PYBD_SF3) and Pyboard-D SF6 (PYBD_SF6), Espruino Pico (ESPRUINO_PICO), etc. As well as several STM32 boards with micropython defined by the community, but less surface, fewer resources running, less stable.

After performing the steps of [~/stm e gcc-arm](https://github.com/micropython/micropython/wiki/Getting-Started-STM#linux-general), enter the directory `ports/stm32`:
```
(base) eduardo@eduardo:~/micropython$ cd ports/stm32
```
It is necessary to compile submodules from `stm32` only in 1st time after downloading or updating the micropython source code:
```
(base) eduardo@eduardo:~/micropython/ports/stm32$ make -j8 submodules
    Use make V=1 or set BUILD_VERBOSE in your environment to increase build verbosity.
    Updating submodules: lib/lwip lib/mbedtls lib/mynewt-nimble lib/stm32lib
```
#### 1.1. Creating Firmware for Pyboard-D SF2 with default configuration (FP32, without threads)
The 'make clean' from the board it is recommended to need every time you create firmware, otherwise it generates very difficult errors to understand, then always use `make clean` of the micropython plate before `make` main:  
```
(base) eduardo@eduardo:~/micropython/ports/stm32$ make BOARD=PYBD_SF2 clean
    Use make V=1 or set BUILD_VERBOSE in your environment to increase build verbosity.
    rm -rf build-PYBD_SF2
```
Compiling and creating firmware, spend a few minutes: 
```
(base) eduardo@eduardo:~/micropython/ports/stm32$ make -j8 BOARD=PYBD_SF2
    ...
    LINK build-PYBD_SF2/firmware.elf
       text	   data	    bss	    dec	    hex	filename
    1000692	    340	  75860	1076892	 106e9c	build-PYBD_SF2/firmware.elf
    INFO: this build requires mboot to be installed first
    INFO: this build places firmware in external QSPI flash
    GEN build-PYBD_SF2/firmware.dfu
    GEN build-PYBD_SF2/firmware.hex
```
#### 1.1.2. Creating firmware for Pyboard-D SF2 with FP64 configuration, without threads

To create double precision firmware (FP64) for floating-point numbers, see [MicroPython v1.12 firmwares for Pyboard v1.1/Lite v1.0/D SF2/D SF3/D SF6 - Optional) Building firmware with 'make' options](https://gitlab.com/rcolistete/micropython-firmwares/-/tree/master/Pyboard/v1.12/2020-07-26#optional-building-firmware-with-make-options), That is, repeat 1.1., however in the `make` command add the `MICROPY_FLOAT_IMPL=double` option:
```
(base) eduardo@eduardo:~/micropython/ports/stm32$ make -j8 MICROPY_FLOAT_IMPL=double BOARD=PYBD_SF2
    ...
    LINK build-PYBD_SF2/firmware.elf
       text	   data	    bss	    dec	    hex	filename
    1013476	    340	  75860	1089676	 10a08c	build-PYBD_SF2/firmware.elf
    INFO: this build requires mboot to be installed first
    INFO: this build places firmware in external QSPI flash
    GEN build-PYBD_SF2/firmware.dfu
    GEN build-PYBD_SF2/firmware.hex
```

#### 1.1.3. Compiling the [**ulab**](https://github.com/v923z/micropython-ulab#ulab) in MicroPython firmware for Pyboard-D SF2

For this command it is necessary that the ulab git clone:

`(base) erosvatis@nucleon-Inspiron-3583:~$ git clone https://github.com/v923z/micropython-ulab.git ulab`

From there we had the memory problem of Pyboard-D SF2-3 to support the ulab in the internal flash. However, in the MicroPython forum, we have another solution published by a user in the ulab topic, "or what you will - numpy on bare metal". We added the line 51 of `micropython/ports/stm32/boards/PYBD_SF2/f722_qspi.ld`:

`*code/*(.text* .rodata*)`

Then, in the directory `~/micropython/ports/stm32`, we execute such command below to build the firmware MicroPython + ulab:

`make -j8 BOARD=PYBD_SF2 USER_C_MODULES=../../../ulab all`

To compile with double precision DP/FP64, execute:

`make -j8 MICROPY_FLOAT_IMPL=double BOARD=PYBD_SF2 USER_C_MODULES=../../../ulab all`

Make sure that there was compilation of the ulab module in the terminal compile log:

```
Use make V=1 or set BUILD_VERBOSE in your environment to increase build verbosity.
Including User C Module from ../../ulab/code
mkdir -p build-PYBD_SF2/genhdr
...
CC ../../ulab/code/ndarray_operators.c
CC ../../ulab/code/ulab_tools.c
CC ../../ulab/code/ndarray.c
CC ../../ulab/code/approx/approx.c
CC ../../ulab/code/compare/compare.c
CC ../../ulab/code/ulab_create.c
CC ../../ulab/code/fft/fft.c
CC ../../ulab/code/fft/fft_tools.c
CC ../../ulab/code/filter/filter.c
CC ../../ulab/code/linalg/linalg.c
CC ../../ulab/code/linalg/linalg_tools.c
CC ../../ulab/code/numerical/numerical.c
CC ../../ulab/code/poly/poly.c
CC ../../ulab/code/vector/vectorise.c
CC ../../ulab/code/user/user.c
CC ../../ulab/code/ulab.c
...
LINK build-PYBD_SF2/firmware.elf
   text	   data	    bss	    dec	    hex	filename
1076244	    400	  76240	1152884	 119774	build-PYBD_SF2/firmware.elf
INFO: this build requires mboot to be installed first
INFO: this build places firmware in external QSPI flash
GEN build-PYBD_SF2/firmware0.bin
GEN build-PYBD_SF2/firmware1.bin
GEN build-PYBD_SF2/firmware.hex
GEN build-PYBD_SF2/firmware.dfu
```
The `firmware.dfu` files are generated in `micropython/ports/stm32/build-PYBD_SF*/`.

To keep ULAB and MICROPYTHON always updated, run the following command within directory `~/micropython/` (to update the MicroPython version) and/or `~micropython/ulab/` (to update the ULAB version):

`git pull`
