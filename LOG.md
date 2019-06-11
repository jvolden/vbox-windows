# VirtualBox Project Log

- [VirtualBox Project Log](#virtualbox-project-log)
  - [Pre-Task](#pre-task)
  - [Tasks for VirtualBox](#tasks-for-virtualbox)
    - [April 23](#april-23)
    - [April 24](#april-24)
    - [April 26](#april-26)
    - [April 27](#april-27)
    - [April 28](#april-28)
    - [May 24](#may-24)
    - [May 28](#may-28)
    - [May 29](#may-29)
    - [May 30](#may-30)
    - [May 31](#may-31)
    - [June 3](#june-3)
    - [June 4](#june-4)
    - [June 5](#june-5)
    - [June 6](#june-6)
    - [June 7](#june-7)
    - [June 11](#june-11)

## Pre-Task

- [X] Compile VirtualBox on Windows

## Tasks for VirtualBox

- [X] Setup development/test environments
- [X] Compile VirtualBox on Windows
- [X] Default to fullscreen VM
- [X] Default to 'save-state' when closing
- [X] Run Portable-VirtualBox with our executable
- [ ] Run VirtualBox without Admin/root access

### April 23

Setup and configured Hyper-V for development environment.

### April 24

Attempt to finish setting up development environment.

### April 26

Installed new hard drive. Old drive died.

### April 27

Finished development environment and got VirtualBox to compile!

### April 28

Finished log formatting and github for review.

### May 24

Start setting up development environment.

### May 28

Finish setting up development environment.

Start compile of VirtualBox. Compiled 64 and 32 bit.

TODO: Create batch files to automate development setup and compilation.

Recompile Portable-VirtualBox AutoIt script using our compiled exe package.

### May 29

Clone and compile Portable-VirtualBox.

New Portable-VirtualBox loads our executable and auto-installs.

Fails to load kernel drivers. VirtualBox error.

Cross checking all dlls and sys files loaded by Portable-VirtualBox

### May 30

Loaded Portable-VirtualBox with official 6.0.4 and it runs. Compared it with my version again.

DRIVER SIGNING

Disabled secure boot and put Windows 10 into test signing mode.

`bcdedit /set testsigning on`

Portable-VirtualBox runs with my executable.

Installed fresh copy of Windows 10 Home on VirtualBox VM.

Start work on auto save-state when closing VirtualBox.

Defaulting to save-state can be done in the .vbox file for the VM.

### May 31

The saving progress bar is gone when auto saving state.

As a hack, put `uisession().saveState()` infront of the save state function call. This is normally called later.

Finished more Windows 10 updates.

Start trying to load VirtualBox without admin/root access.

### June 3

Run in userspace?

### June 4

Continue trying to run in userspace.

Trying cflags that may effect how virtualization works.

Contacted devs on irc.freenode.net #vbox-dev, said it was not possible.

How does TinyEMU work? Compiling on win32 is not completed yet.

### June 5

Implement compiling on win32.

<sys/select.h> needed for windows. winsock2.h does some of the functions but not all.

libslirp.h not ported to win32.

Shelved TinyEMU for now.

Revisited qemu. Can we speed it up without elevated privleges?

Windows 10 install took >1h.

```bash
qemu-system-x86_64.exe
  -hda c:\devel\qemu-machines\win10.img
  -boot d
  -cdrom c:\users\jon\downloads\windows.iso
  -m 2G
```

Try using new WHPX accelerator.

```bash
-accel whpx
```

Took longer to install than without. When using 64bit binaries whpx support is said to be `untested`.

Windows won't finish install. Stops after reboot and soft locks.

### June 6

Compile qemu with whpx for windows.

Needs to be cross compiled from a linux environment using mingw32/64. Does not work through wsl ubuntu.

mingw glib libraries are not compatible with newest source.

Back to virtualbox. If we accept admin access must be required can we verify drivers from autoit script.

```bash
vboxdrv.inf
vboxdrv.cat
vboxdrv.sys
```

### June 7

Make host installer with minimum number of files to get virtualbox running.

Easiest is to just install virtualbox?

Host much have hypervisor disabled, or vbox will not run with acceleration.

In virtualbox out/build folder, comregister.cmd loads the virtualbox service. The service is needed to access com components.

Use seperate installer or have autoit do it and make it leave the files inplace instead of removing them on close?

Autoit has crypt.au3 functions to verify hashes of files.

```autoit
_Crypt_HashFile(file, algorithm)
```

Check vboxdrv.sys file, if they are different, exit or overwrite. (Need admin)

### June 11

