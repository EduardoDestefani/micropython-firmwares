# micropython-firmwares
Repositório de Firmwares personalizados.

### Firmwares STM32 placas Pyboard-D SF2
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20Pyboard-D%20SF2).

- `pybd-sf2_dp_v1.12-665-g60f5b941e_2020-08-22.dfu` ; firmware com precisão dupla nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP).  
- `pybd-sf2_sp_144mhz_v1.12-665-g60f5b941e_2020-08-22.dfu` ; firmware com precisão simples (SP) e clock default de 144MHz.
- `pybd-sf2_sp_thread_v1.12-657-g37e1b5c89_2020-08-22.dfu` ; firmware permitindo multithreading com precisão simples (SP).
- `pybd-sf2_sp_v1.12-665-g60f5b941e_2020-08-22.dfu` ; firmware com precisão simples nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP).
- `pybd-sf2_sp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão simples nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). MicroPython v1.15 e ulab v2.8.3-2D.
- `pybd-sf2_dp_v1.15-154-g6a127810c-ulab_v2.8.3-2D_20210526.dfu`; firmware com precisão dupla nativa (Pyboard-D SF2 possui suporte em hardware apenas para FP32/SP). MicroPython v1.15 e ulab v2.8.3-2D.

Os arquivos 'firmware.dfu' são gerados em 'micropython/ports/stm32/build-PYBD_SF2/'. 
Utilize o comando `sudo python3 pydfu.py -u nome_do_firmware.dfu`, instale o firmware em sua placa.


### Firmwares nRF placas BBC Micro:bit
Firmwares disponíveis [aqui](https://github.com/EduardoDestefani/micropython-firmwares/tree/master/Firmwares%20BBC%20Microbit).

- `microbit_v1.12-665-g60f5b941e_2020-08-22.hex` ; firmware com micropython atualizado (v1.12).

Os arquivos 'firmware.hex' (.bin, .elf) são gerados em 'micropython/ports/nrf/build-microbit/'.
Pegue o arquivo '.hex' e arraste para o pseudo pendrive "MICROBIT".
