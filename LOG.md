# VirtualBox Project Log

- [VirtualBox Project Log](#VirtualBox-Project-Log)
  - [Pre-Task](#Pre-Task)
  - [Tasks for VirtualBox](#Tasks-for-VirtualBox)
    - [April 23](#April-23)
    - [April 24](#April-24)
    - [April 26](#April-26)
    - [April 27](#April-27)
    - [April 28](#April-28)
    - [May 24](#May-24)
    - [May 28](#May-28)
    - [May 29](#May-29)
    - [May 30](#May-30)
    - [May 31](#May-31)
    - [June 3](#June-3)
    - [June 4](#June-4)
    - [June 5](#June-5)
    - [June 6](#June-6)
    - [June 7](#June-7)
    - [June 11](#June-11)
    - [June 12](#June-12)
    - [June 13](#June-13)
    - [June 14](#June-14)
    - [June 17](#June-17)
    - [June 18](#June-18)
    - [June 19](#June-19)
    - [June 20](#June-20)
    - [June 21](#June-21)
    - [June 24](#June-24)
    - [June 25](#June-25)
    - [June 26](#June-26)
    - [June 27](#June-27)
    - [June 28](#June-28)
    - [July 1](#July-1)
    - [July 2](#July-2)

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

Edit autoit script to leave drivers installed if we installed them on the system.

Break script into modules.

__Lots of refactoring__

Create standalone exe. Put vbox.exe installer on drive?

### June 12

Update usb stick with latest files.

user/pass: ku/ku1234 test machine

Can't move from one machine to another during a save state/snapshot. Normal behavior?

Using official release 6.0.4+:
  We don't need to sign drivers
  We don't need admin access

Determine DLLs needed for virtual box at a minimum.

Make resolutions match automaticly to host machine

Xen?

### June 13

Remove hybrid mode. Portable-virtualbox runs files off host machine and exits if they are already install. We need to verify files to ensure our machine works with their drivers.

Hybrid mode forgets portable-virtualbox settings like automaticly starting a machine if set in settings.

Added debug window to portable-virtualbox. Finished some refactoring and uploaded/forked git.

[Portable-Virtualbox](https://github.com/jvolden/portable-virtualbox)

_Unfinished: Needs to be updated_

Moved to QEMU with hypervisor?

Meeting with Matt.

Waiting for contact at library to finish fleshing out specs for host/guest machine settings.

Features? Browser Security. Brave?

Update goals?

### June 14

Finish implementing debug logging.

Lots of code/refactoring.

### June 17

Testing on different machines at home.

### June 18

Started native builds of QEMU for windows on windows 10 using msys2 with WHPX enabled.

Same install speed at pre-build binaries. Too slow.

### June 19

Install/create windows isntall on virtualbox and convert it to qcow for qemu

`> qemu-img convert windows10.img -O qcow2 qemu\windows10.img`

Won't boot to Windows completely. Freezes after 20 min

Doesn't work on mobile intel processors? [todo]

Runs on desktops with `ok`(?) speed compared to Virtualbox.

autoit function to build usable command on windows.

```AutoIt
Func _Run_Command()
  Local $command 
  $command &= $G_QEMUEXE
  $command &= " -hda " & $G_WINDOWSIMG
  $command &= " -boot d"
  $command &= " -usb -device usb-tablet"
  $command &= " -accel whpx"
  $command &= " -machine q35"
  $command &= " -cpu qemu64"
  $command &= " -m 3G"
  $command &= " -full-screen"
  Return $command
EndFunc
```

Still can't savevm. No possible? Prevents portability conflicts between hosts?

### June 20

Have test windows machine installed.

Runs fairly slow with 6G memory.

Start looking at cpu flags for savevm?

### June 21

Explorer ways to speed up windows 10 default installation.

Debloat/updates?

Reinstalling Windows 10 with newest updates. Takes too long to update manually.

Disable windows updates?

### June 24

Create bench setup with puppylinux.

Switched to archlinux.

Using linux bench scripts.

`wget -qO- bench.sh | bash`

[haydenjames](https://github.com/haydenjames/bench-scripts)

### June 25

Goals:  
- [ ] Hotswappable
- [ ] Auto-run (installable exe?)

Begin autoit script to check host system for QEMU to run.

Check for:

* CPU
* Memory
* Hypervisor
* Network
* USB Speed?

### June 26

Work on autoit to determine USB capabilities

Windows doesn't report directly USB protocols supported by inserted device.

### June 27

Switch to c++/# to use native win api to query usb devices?

### June 28

Shelving USB query for now. Use a more brute force test to determine speed?

File reads/writes speeds, maybe doesn't need to be 3.0?

### July 1

Return to finishing autoit script for qemu.

Added loading/splash screen. More/less info for user?

### July 2

