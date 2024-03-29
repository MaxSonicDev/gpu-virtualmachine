# My configuration for my virtual machine with GPU Passthrough

![Screenshot from 2022-04-18 12-41-43](https://user-images.githubusercontent.com/36816420/163797379-64732d4e-8980-47ab-8e80-cb688dd19df6.png)
*Screenshot of Windows Guest run on the Fedora Host (Remote control with Parsec)*

## Introduction

This is just a repo for make a backup of files and instruction to make a optimized KVM Virtual Machine with PCI-E Passthrough. This virtual machine is optimized for gaming use.

## Host

- OS: Arch Linux
- Kernel: 6.2.5-zen
- Motherboard: X470 AORUS ULTRA GAMING
- CPU: AMD Ryzen 9 3900X
- Memory: 128 Go DDR4 @ 3200 Mhz
- GPU 1: AMD Radeon 6900 XT
- GPU 2: Nvidia GeForce GTX 1070 (for guest)
- NVMe 1: Crucial P3 2 To
- NVMe 2: Crucial P5 2 To (for guest)
- Other Storage device : Samsung 870 QVO 1 To, Samsung 870 EVO 1To and Crucial MX500 1 To

## Guest

- OS: Microsoft Windows 11 Enterprise Insider 22H2 (22581.200)
- CPU: 4C/8T
- Memory: 32 Go
- GPU: Nvidia Geforce GTX 1070
- NVMe : Crucial P5 2 To
- Other devices : ASMedia ASM1143 USB 3.1 Host Controller

## Todo 

- Hugepages
- Upload actual XML Configuration
- Windows Optimization 
- Audio Setup with Scream
- Command host for Virtual Machine
- Setup bridge on Network Manager
- CPU Pinning 
