---
layout: default
title: Unit 1
permalink: /notes/os/unit1
lastmod: 2026-09-02
---

# Unit 1
Before we do anything, I have to mention that these notes will not be friendly or even comprehensible. They are mostly a record of what I found useful while taking this course. For more polished explanations, [Prof. Hakner's course website](https://faculty.cooper.edu/hak/ece357/) is a good place to look. This course has ECE251 (Computer Architecture) as a prerequisite.

I will use this [GitHub Repository](https://github.com/hoseony/ECE357-Operating-Systems) for my homework solutions and this website to talk about basically whatever I feel like talking about. I will still try to make these as nutritious as possible…

Since most of the conceptual part is already explained well in the course notes, I will focus primarily on the practical stuff that is helpful for the problem sets.

## Setting up Environment
If you are happen to be the blessed one who found a way into running Linux as Operating System, you are all good. This segment is dedicated to those unfortunate souls (like myself).

Yes, you can use the machine from the school, but it does have limitation. So, what I decided on was using QEMU (virtual machine) to run Ubuntu server locally. I have previously used VirtualBox. It is indeed easier to use, but QEMU gives more control (putting it simply). So I will show you the way I configured my QEMU here (I am also a beginner, so let me know if there's better way of doing this).

The goal of this would be `macOS -> QEMU -> Ubuntu Server VM -> ssh`
```
brew install qemu 
qemu-system-aarch64 --version
```
Grab official arm Ubuntu server.
e.g. `ubuntu-26.04.1-live-server-arm64.iso`

Create a directory:
```
mkdir -p ~/VMs/ubuntu
cd ~/VMs/ubuntu
```
Put the .iso into this directory.
e.g. `~/VMs/ubuntu/ubuntu-26.1-live-server-arm64.iso`

Create a virtual disk.

```
qemu-img create -f qcow2 ubuntu.qcow2 30G
```

Start the server with

```
qemu-system-aarch64 \
  -machine virt \
  -cpu host \
  -accel hvf \
  -smp 4 \
  -m 4G \
  -bios "$(brew --prefix qemu)/share/qemu/edk2-aarch64-code.fd" \
  -drive file="$HOME/VMs/ubuntu/ubuntu.qcow2",if=virtio,format=qcow2 \
  -cdrom "$HOME/VMs/ubuntu/ubuntu-26.04.1-live-server-arm64.iso" \
  -device virtio-net-pci,netdev=net0 \
  -netdev user,id=net0,hostfwd=tcp:127.0.0.1:2222-:22 \
  -nographic
```

Then, the Ubuntu server installer will appear. Most of cases, the default is fine. Few things I had to change were storage (since it did not use the 30GB that I allocated) and SSH setting. For username and password, just make sure you know it.

```
ssh -p 2222 username@localhost
```
