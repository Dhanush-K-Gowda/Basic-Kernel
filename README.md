<h1 align="center" id="title">Basic Kernel in C</h1>

<p align="center"><img src="https://socialify.git.ci/Dhanush-K-Gowda/Basic-Kernel/image?description=1&amp;font=Source%20Code%20Pro&amp;language=1&amp;name=1&amp;owner=1&amp;pattern=Charlie%20Brown&amp;theme=Auto" alt="project-image"></p>


<h2>🖼️ Project Screenshot:</h2>

<img src="https://github.com/Dhanush-K-Gowda/Basic-Kernel/blob/main/demo.png" alt="project-screenshot">

<h2>🛠️ Build and run:</h2>

<p>1. Run in emulator</p>

```
qemu-system-i386 -kernel kernel
```

<p>2. Build</p>

```
nasm -f elf32 kernel.asm -o kasm.o
gcc -m32 -c kernel.c -o kc.o
ld -m elf_i386 -T link.ld -o kernel kasm.o kc.o
```

<h2>✍️ Acknowledgement</h2>

[Thanks to this blogpost](https://arjunsreedharan.org/post/82710718100/kernels-101-lets-write-a-kernel)
