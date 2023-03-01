---
title: "Booting a minimal Linux system in QEMU"
date: 2022-12-11T22:29:50-06:00
lastmod: 2022-12-11T22:30:00-06:00
draft: false
---
# Introduction
- What?

In this guide we'll be exploring how to boot an extremely minimal Linux system using QEMU. The goal is to understand what pieces make up a minimal Linux system and how to change the behavior of the components.

- Why?

Our goal is to learn by doing. In particular, we want to enable experimentation.

---

## Prerequisites
- Linux System
    This guide requires some kind of modern Linux. This can take the form of a bare-metal Linux install, a virtual machine, WSL on Windows, or even Docker for Mac or Docker for Windows.
- Linux Kernel Source
    Download from https://kernel.org as a tarball or perform a Git clone.
- QEMU
    - macOS
    - Windows
    - Linux
- Rust Compiler
    - New to this? Use rustup.

## High-level Plan
- Create Linux Kernel Config
- Compile Kernel (at least, start compilation)
- Create Cargo Project