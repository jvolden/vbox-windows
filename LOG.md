# VirtualBox Project Log

- [VirtualBox Project Log](#virtualbox-project-log)
  - [Pre-Task](#pre-task)
    - [April 23](#april-23)
    - [April 24](#april-24)
    - [April 26](#april-26)
    - [April 27](#april-27)
    - [April 28](#april-28)
  - [Tasks for VirtualBox](#tasks-for-virtualbox)
    - [May 24](#may-24)
    - [May 28](#may-28)
    - [May 29](#may-29)
    - [May 30](#may-30)
    - [May 31](#may-31)
    - [June 3](#june-3)

## Pre-Task

- [X] Compile VirtualBox on Windows

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

## Tasks for VirtualBox

- [X] Setup development/test environments
- [X] Compile VirtualBox on Windows
- [X] Default to fullscreen VM
- [X] Default to 'save-state' when closing
- [X] Run Portable-VirtualBox with our executable
- [ ] Run VirtualBox without Admin/root access

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