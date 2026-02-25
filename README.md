# LoRaM3-D_templates

IDE Templates for LoRaM3-D board with SW4STM32 (System Workbench for STM32), these templates are ready to use and setup for STLink debugger.

How to build and flash on the command line:

```
cd LoRaM3_F303_HAL_OLED_LORA/Debug
make LoRaM3_F303_HAL_OLED_LORA.elf
dfu-util --alt 0 --dfuse-address 0x08000000 -D LoRaM3_F303_HAL_OLED_LORA.bin 
```

It should reproduce the test messages on the OLED, via serial at 115200,
and maybe some LoRa packets as well.

