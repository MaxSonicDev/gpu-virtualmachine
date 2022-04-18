# My configuration for my virtual machine with GPU Passthrough

## Host

- OS: Fedora Linux 36 Workstation Edition
- Kernel: 5.17.2-300.fc36.x86_64 
- Motherboard: X470 AORUS ULTRA GAMING
- CPU: AMD Ryzen 9 3900X
- Memory: 64 Go DDR4 @ 3000 Mhz
- GPU 1: AMD Radeon 6600 XT
- GPU 2: Nvidia GeForce GTX 1070 (for guest)
- NVMe 1: PNY CS2130 1 To
- NVMe 2: Crucial P5 2 To (for guest)
- Other Storage device : Crucial BX500 480 Go + Samsung 870 QVO 1 To 

## Guest

- OS: Microsoft Windows 11 Enterprise Insider 22H2 (22581.200)
- CPU: 4C/8T
- Memory: 16 Go
- GPU: Nvidia Geforce GTX 1070
- NVMe : Crucial P5 2 To
- Other devices : ASMedia ASM1143 USB 3.1 Host Controller

## Todo 

- Evdev Passthrough
- Hugepages
- Upload actual XML Configuration
- Windows Optimization 
- Audio Setup with Scream
- Command host for Virtual Machine
