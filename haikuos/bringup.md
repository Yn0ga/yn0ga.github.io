---
layout: default
---

# QEMU matrix

Difference in Qemu version & parameters may leads to (very) different outcome so, here's my 2cts 

 
## Common commmand line : 
```
qemu-system-ppc -L pc-bios -boot d -display sdl -m 1G -drive file=haiku-boot-cd.iso,format=raw,media=cdrom -drive file=haiku-minimum.image,format=raw,media=disk -prom-env "auto-boot?=true" -serial mon:stdio
```

## Parameter matrix : 
| Version | Bootloader | Partitions | Kernel | Host OS | Parameters | Details |
| :---: | :---: | :---: | :---: | :---: | :--- | :---: |
| 7.1.0 | ✅ | ✅ | ✅ | Win64 | | CPU type PowerPC,750 |
| 7.1.0 | ✅ | ✅ | ✅ | Win64 | --nographic | CPU type PowerPC,750 |
| 7.1.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 | |
| 7.1.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 --nographic | |
| 7.1.0 | ✅ | 🛑 | 🛑 | Win64 | -cpu G4 -M mac99 --nographic | |
| 7.1.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 -device ati-vga | |
| 7.2.20 | ✅ | 🛑 | 🛑 | Linux | | CPU type PowerPC,750 |
| 7.2.20 | ✅ | ✅ | ✅ | Linux | --nographic | CPU type PowerPC,750 |
| 7.2.20 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 | |
| 7.2.20 | ✅ | ✅ | ✅ | Linux | -cpu G4 --nographic | |
| 7.2.20 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 -M mac99 --nographic | |
| 7.2.20 | ✅ | ✅ | ✅ | Linux | -cpu G4 -device ati-vga | |
| 8.2.0 | ✅ | ✅ | ✅ | Win64 | | CPU type PowerPC,750 |
| 8.2.0 | ✅ | ✅ | ✅ | Win64 | --nographic | CPU type PowerPC,750 |
| 8.2.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 | |
| 8.2.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 --nographic | |
| 8.2.0 | ✅ | 🛑 | 🛑 | Win64 | -cpu G4 -M mac99 --nographic | |
| 8.2.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 -device ati-vga | |
| 8.2.2 | ✅ | 🛑 | 🛑 | Linux | | CPU type PowerPC,750 |
| 8.2.2 | ✅ | ✅ | ✅ | Linux | --nographic | CPU type PowerPC,750 |
| 8.2.2 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 | |
| 8.2.2 | ✅ | ✅ | ✅ | Linux | -cpu G4 --nographic | |
| 8.2.2 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 -M mac99 --nographic | |
| 8.2.2 | ✅ | ✅ | ✅ | Linux | -cpu G4 -device ati-vga | |
| 9.2.4 | ✅ | 🛑 | 🛑 | Linux | | CPU type PowerPC,750 |
| 9.2.4 | ✅ | ✅ | ✅ | Linux | --nographic | CPU type PowerPC,750 |
| 9.2.4 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 | |
| 9.2.4 | ✅ | ✅ | ✅ | Linux | -cpu G4 --nographic | |
| 9.2.4 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 -M mac99 --nographic | |
| 9.2.4 | ✅ | ✅ | ✅ | Linux | -cpu G4 -device ati-vga | |
| 10.1.0 | ✅ | 🛑 | 🛑 | Linux | | CPU type PowerPC,750 |
| 10.1.0 | ✅ | ✅ | ✅ | Linux | --nographic | CPU type PowerPC,750 |
| 10.1.0 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 | |
| 10.1.0 | ✅ | ✅ | ✅ | Linux | -cpu G4 --nographic | |
| 10.1.0 | ✅ | 🛑 | 🛑 | Linux | -cpu G4 -M mac99 --nographic | |
| 10.1.0 | ✅ | ✅ | ✅ | Linux | -cpu G4 -device ati-vga | |
| 10.1.0 | ✅ | ✅ | ✅ | Win64 | | CPU type PowerPC,750 |
| 10.1.0 | ✅ | ✅ | ✅ | Win64 | --nographic | CPU type PowerPC,750 |
| 10.1.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 | |
| 10.1.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 --nographic | |
| 10.1.0 | ✅ | 🛑 | 🛑 | Win64 | -cpu G4 -M mac99 --nographic | |
| 10.1.0 | ✅ | ✅ | ✅ | Win64 | -cpu G4 -device ati-vga | |

## Partitions issue

On my end, if I deviate from those parameters, QEMU locks up at this stage : 
<img width="810" height="632" alt="image" src="https://github.com/user-attachments/assets/84fa996c-1331-4858-b399-3611d42515e7" />

(Didn't check the precise error yet) 

# TL;DR: 

Regardless of your host OS (windows or linux), your qemu command line should looks like this : 

For graphical mode 
```
qemu-system-ppc -L pc-bios -boot d -display sdl -m 1G -serial mon:stdio -device ati-vga -prom-env "auto-boot?=true" -drive file=haiku-boot-cd.iso,format=raw,media=cdrom -drive file=haiku-minimum.image,format=raw,media=disk" 
```

For command line mode 

```
qemu-system-ppc -L pc-bios -boot d -display sdl -m 1G -serial mon:stdio -device ati-vga --nographic -prom-env "auto-boot?=true" -drive file=haiku-boot-cd.iso,format=raw,media=cdrom -drive file=haiku-minimum.image,format=raw,media=disk" 
```



