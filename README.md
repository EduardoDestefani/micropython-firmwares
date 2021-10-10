# micropython-firmwares
Repositório de Firmwares personalizados.

### Instalação dos firmwares em Pyboard D-series

Para saber como instalar os firmwares do repositório, basta executar tais comandos com o Pyboard-D no modo "dfu". O comando deve ser executado no mesmo diretório em que os arquivos [pydfu.py](https://github.com/EduardoDestefani/micropython-firmwares/blob/master/Firmwares%20Pyboard-D%20SF2/pydfu.py) e 'firmware.dfu' estão, comando:

`sudo python3 pydfu.py -u firmware_name.dfu`

### Firmwares STM32 para placas Pyboards-D SF2
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF2).

- `pybd-sf2_dp_v1.12-665-g60f5b941e_2020-08-22.dfu` ; firmware com precisão dupla nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP).  
- `pybd-sf2_sp_144mhz_v1.12-665-g60f5b941e_2020-08-22.dfu` ; firmware com precisão simples (SP) e clock default de 144MHz.
- `pybd-sf2_sp_thread_v1.12-657-g37e1b5c89_2020-08-22.dfu` ; firmware permitindo multithreading com precisão simples (SP).
- `pybd-sf2_sp_v1.12-665-g60f5b941e_2020-08-22.dfu` ; firmware com precisão simples nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP).
- `pybd-sf2_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão simples nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.15** e **ulab v2.8.3-2D**.
- `pybd-sf2_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão dupla nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.15** e **ulab v2.8.3-2D**.
- `pybd-sf2_sp_v1.16-39-g4ada56d4c-ulab_v3.1.1-2D-20210703.dfu`; firmware com precisão simples nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.16** e **ulab v3.1.1-2D**.
- `pybd-sf2_dp_v1.16-39-g4ada56d4c-ulab_v3.1.1-2D-20210703.dfu`; firmware com precisão dupla nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.16** e **ulab v3.1.1-2D**.
- `pybd-sf2_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware com precisão dupla nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.16** e **ulab v3.3.4-2D**.

### Firmwares STM32 para placas Pyboard-D SF3
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF3).

- `pybd-sf3_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão simples nativa (Pyboard-D SF3 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.15** e **ulab v2.8.3-2D**.
- `pybd-sf3_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão dupla nativa (Pyboard-D SF3 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.15** e **ulab v2.8.3-2D**.
- `pybd-sf3_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware com precisão dupla nativa (Pyboard-D SF3 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.16** e **ulab v3.3.4-2D**.

### Firmwares STM32 para placas Pyboard-D SF6
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF6).

- `pybd-sf6_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão simples nativa (Pyboard-D SF6 possui suporte em hardware para FP32/SP e FP64/DP). **MicroPython v1.15** e **ulab v2.8.3-2D**.
- `pybd-sf6_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão dupla nativa (Pyboard-D SF6 possui suporte em hardware para FP32/SP e FP64/DP). **MicroPython v1.15** e **ulab v2.8.3-2D**.
- `pybd-sf6_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware com precisão dupla nativa (Pyboard-D SF6 possui suporte em hardware para FP32/SP e FP64/DP). **MicroPython v1.16** e **ulab v3.3.4-2D**.

### Firmwares STM32 para placas Pyboard v1.1
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard%20v1.1).

- `pyb-v1.1_sp_v1.17-39-g4ada56d4c-ulab_v3.3.4-2D-20210918.dfu`; firmware com precisão dupla nativa (Pyboard v1.1 possui suporte em hardware apenas para FP32/SP). **MicroPython v1.16** e **ulab v3.3.4-2D**.

### Firmwares nRF placas BBC Micro:bit
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20BBC%20Microbit).

- `microbit_v1.12-665-g60f5b941e_2020-08-22.hex` ; firmware com micropython atualizado (v1.12).

Os arquivos 'firmware.hex' (.bin, .elf) são gerados em 'micropython/ports/nrf/build-microbit/'.
Pegue o arquivo '.hex' e arraste para o pseudo pendrive "MICROBIT".

### Construção dos firmwares ulab para placas Pyboard
No Debian e derivados o gcc-arm é muito antigo (5.x) no repositório oficial. Então instalar manualmente gcc-arm atual, seguir ["Getting Started STM"](https://github.com/micropython/micropython/wiki/Getting-Started-STM). A versão escolhida foi a [gcc-arm-none-eabi-9-2020-q2-update-x86_64-linux.tar.bz2](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads).

Adicionar ao final do arquivo .bashrc (execute `sudo nano ~/.bashrc`) :

`export PATH="${PATH}:${HOME}/stm/gcc-arm-none-eabi-9-2020-q2-update/bin`

Outras dependências são necessárias, recomenda-se instalar uma a uma, e então executar um `sudo apt-get update`. Logo, execute :

```
sudo apt-get install git

sudo apt-get install build-essential 

sudo apt-get install libreadline-dev 

sudo apt-get install libffi-dev 

sudo apt-get install pkg-config
```
Compilando MicroPython mainline (principal) para [Unix/Linux](https://github.com/micropython/micropython/wiki/Getting-Started):

* Com git, compilador gcc, etc instalados, escolha um diretório e execute os comandos:

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

#### 1. Compilando micropython/ports/stm32 (para placas Pyboard, etc)
Escolhemos a [placa Pyboard D SF2](https://store.micropython.org/product/PYBD-SF2-W4F2), definida em 'micropython/ports/stm32/boards/PYBD_SF2', tal que `BOARD=PYBD_SF2`.  
Mas há outras placas MicroPython oficiais, como Pyboard v1.1 (PYBV11), Pyboard Lite v1.0 (PYBLITEV10), Pyboard D SF33 (PYBD_SF3) e Pyboard D SF6 (PYBD_SF6), Espruino Pico (ESPRUINO_PICO), etc. Bem como várias placas STM32 com MicroPython definido pela comunidade, porém com menos surporte, menos recursos funcionando, menos estáveis.

Após realizar os passos de [~/stm e gcc-arm](https://github.com/micropython/micropython/wiki/Getting-Started-STM#linux-general), entre no diretório `ports/stm32` :
```
(base) eduardo@eduardo:~/micropython$ cd ports/stm32
```
É necessário compilar submódulos do `stm32` só na 1a vez após fazer download ou atualização do código-fonte MicroPython :
```
(base) eduardo@eduardo:~/micropython/ports/stm32$ make -j8 submodules
    Use make V=1 or set BUILD_VERBOSE in your environment to increase build verbosity.
    Updating submodules: lib/lwip lib/mbedtls lib/mynewt-nimble lib/stm32lib
```
##### 1.1. Criando firmware para Pyboard-D SF2 com configuração default (FP32, sem threads)
O 'make clean' da placa é recomendado a necessário toda vez que for criar firmware, senão gera erros bem difíceis de  entender, então sempre use `make clean` da placa MicroPython antes do `make` principal:  
```
(base) eduardo@eduardo:~/micropython/ports/stm32$ make BOARD=PYBD_SF2 clean
    Use make V=1 or set BUILD_VERBOSE in your environment to increase build verbosity.
    rm -rf build-PYBD_SF2
```
Compilando e criando firmware, gasta alguns poucos minutos:  
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
##### 1.1.2. Criando firmware para Pyboard-D SF2 com configuração FP64, sem threads

Para criar firmare com precisão dupla (FP64) para números de ponto flutuante, vide 
[MicroPython v1.12 firmwares for Pyboard v1.1/Lite v1.0/D SF2/D SF3/D SF6 - Optional) Building firmware with 'make' options](https://gitlab.com/rcolistete/micropython-firmwares/-/tree/master/Pyboard/v1.12/2020-07-26#optional-building-firmware-with-make-options), ou seja, repetir 1.1., porém no comando `make` adicionar a opção `MICROPY_FLOAT_IMPL=double` :
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

##### 1.1.3. Compilando o [**ulab**](https://github.com/v923z/micropython-ulab#ulab) no firmware MicroPython para Pyboard-D SF2

Para tal comando é necessário que o git clone do ulab seja feito dentro do diretório `micropython/`:

`git clone https://github.com/v923z/micropython-ulab.git ulab`

A partir daí tivemos o problema de memória do Pyboard-D SF2-3 para sustentar o ulab na flash interna. Porém, no fórum micropython, temos outra solução publicada por um usuário no tópico ulab, "or what you will - numpy on bare metal". Adicionamos a linha 51 de `micropython/ports/stm32/boards/PYBD_SF2/f722_qspi.ld` o comando:

`*code/*(.text* .rodata*)`

Logo, no diretório `~/micropython/ports/stm32`, executamos tal comando abaixo para construir o firmware MicroPython + ulab:

`make -j8 BOARD=PYBD_SF2 USER_C_MODULES=../../ulab all`

Para compilar com precisão dupla DP/FP64, execute:

`make -j8 MICROPY_FLOAT_IMPL=double BOARD=PYBD_SF2 USER_C_MODULES=../../ulab all`

Certifique-se que houve a compilação do módulo ulab no log de compilação do terminal:

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
Os arquivos 'firmware.dfu' são gerados em 'micropython/ports/stm32/build-PYBD_SFx/'.

Para manter o ulab e o Micropython sempre atualizados, execute o comando a seguir dentro do diretório `~/micropython/` (para atualizar a versão do MicroPython) ou `~micropython/ulab/` (para atualizar a versão do ulab):

`git pull`
