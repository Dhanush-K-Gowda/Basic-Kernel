# Simple 16-bit Bootloader

This repository contains a basic **16-bit bootloader** written in **NASM assembly**, which prints "Hello world!" to the screen using BIOS interrupts. It is designed to run on x86 real-mode systems and can be tested using **QEMU**.

## Features
- Runs in **real mode (16-bit)**
- Uses BIOS interrupt **0x10** to print text
- Properly structured boot sector with **0xAA55 signature**
- Fits within **512 bytes** (boot sector size requirement)

## Prerequisites
Ensure you have the following installed:
- **NASM** (Netwide Assembler)
- **QEMU** (for emulation)

To install NASM and QEMU on **Ubuntu/WSL**, run:
```bash
sudo apt update && sudo apt install -y nasm qemu-system-x86
```

## Building and Running
### 1. Assemble the Bootloader
```bash
nasm -f bin bootloader.asm -o boot.bin
```

### 2. Run with QEMU
For x86 emulation:
```bash
qemu-system-x86_64 -drive format=raw,file=boot.bin
```
For **better compatibility** with 16-bit code:
```bash
qemu-system-i386 -drive format=raw,file=boot.bin
```

### 3. (Optional) Run in QEMU without GUI
```bash
qemu-system-i386 -nographic -drive format=raw,file=boot.bin
```

## Code Explanation
### `bootloader.asm`
```assembly
bits 16        ; 16-bit mode
org 0x7c00     ; BIOS loads bootloader at 0x7C00

boot:
    mov si, hello  ; Load message address
    mov ah, 0x0e   ; BIOS TTY mode (teletype output)
.loop:
    lodsb          ; Load byte from SI into AL
    or al, al      ; Check for null terminator
    jz halt        ; If null, halt
    int 0x10       ; BIOS interrupt to print character
    jmp .loop
halt:
    cli            ; Disable interrupts
    hlt            ; Halt CPU

hello: db "Hello world!", 0

times 510 - ($-$$) db 0  ; Pad sector to 512 bytes
dw 0xaa55                ; Boot sector signature
```

## Notes
- This bootloader is **not an OS**; it simply prints a message and halts.
- It runs in **real mode**, so there is **no access to modern OS features**.
- You can extend it to load a second-stage bootloader or an OS kernel.

## License
This project is licensed under the **MIT License**. Feel free to modify and extend!

## Contribution
Pull requests are welcome! If you find issues or want to improve the code, feel free to contribute.
