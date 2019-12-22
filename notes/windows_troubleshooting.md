# Windows Boot Process

Windows 10 boot process on BIOS systems comprises of four major phases. It starts from POST and ends up in loading the Windows OS Loader or the Kernel. Here is the list of stages it goes through:

1. PreBoot
2. Windows Boot Manager
3. Windows OS Loader.
4. Windows NT OS Kernel.

During every process, a program is loaded. Depending on whether it uses Legacy BIOS or UEFI, the file paths and files change.

| Phase  | Boot Process | BIOS | UEFI |
| ------------- | ------------- | ------------- | ------------- |
| 1  | PreBoot | MBR/PBR (Bootstrap Code) | UEFI Firmware |
| 2  | Windows Boot Manager | `%SystemDrive%\bootmgr` | `\EFI\Microsoft\Boot\bootmgfw.efi` |
| 3  | Windows OS Loader | `%SystemRoot%\system32\winload.exe` | `%SystemRoot%\system32\winload.efi` |
| 4  | Windows NT OS Kernel | `%SystemRoot%\system32\ntoskrnl.exe` | |

1. **PreBoot**: POST or Power-On Self-Test loads firmware settings. It checks for a valid disk system, and if the system is good to go for the next phase. If the computer has a valid MBR, i.e., Master Boot Record, the boot process moves further and loads Windows Boot Manager.
2. **Windows Boot Manager**: This step determines if you have multiple OS installed on your computer. If yes, then it offers a menu with the names of the OSs. When you select the OS, it will load the right program, i.e., Winload.exe to boot you into the correct OS.
3. **Windows OS Loader**: Like its name, WinLoad.exe loads important drivers to kick start the Windows Kernel. The kernel uses the drivers to talk to the hardware and do rest of the things required for the boot process to continue.
4. **Windows NT OS Kernel**: This is the last stage which picks up the Registry settings, additional drivers, etc. Once that has been read, the control is taken by the system manager process. It loads up the UI, the rest of the hardware and software. That’s when you finally get to see your Windows 10 Login screen.

When you run Windows 10 on a computer that supports Unified Extensible Firmware Interface (UEFI), Trusted Boot protects your computer from the moment you power it on. When the computer starts, it first finds the operating system bootloader. Computers without Secured Boot simply run whatever bootloader is on the PC’s hard drive. When a computer equipped with UEFI starts, it first verifies that the firmware is digitally signed. If Secure Boot is enabled, the firmware examines the bootloader’s digital signature to verify that it is intact hasn’t been modified.

# Abbreviations

BIOS (Basic Input/Output System): BIOS checks the health of your computer's hardware and allows Windows to start. When you turn on your PC, its BIOS runs a POST to ensure that the machine's devices (hard drive, sound card, keyboard, and the like) are connected and working properly. If the test finds no problems, the BIOS turns over control of your PC to another piece of software, typically the "operating system".

POST (Power-On Self-Test): POST is the diagnostic testing sequence that a computer's basic input/output system (or "starting program") runs to determine if the computer keyboard, random access memory, disk drives, and other hardware are working correctly.

UEFI (Unified Extensible Firmware Interface): UEFI is a specification for a software program that connects a computer's firmware to its operating system (OS). UEFI is expected to eventually replace BIOS. Like BIOS, UEFI is installed at the time of manufacturing and is the first program that runs when a computer is turned on.

EFI (Extensible Firmware Interface): A file with the EFI file extension is an Extensible Firmware Interface file. EFI files are boot loader executables, exist on UEFI (Unified Extensible Firmware Interface) based computer systems, and contain data on how the boot process should proceed.

## Troubleshooting Process and Tools

- Gather
- Plan of Action
- Remediate
- Document
- Tools

Using the Task Manager, Resource Monitor, and Performance Monitor

Using Reliability History, Event Viewer, and Steps Recorder.

# Boot Process

# Resolving BCD (Boot Configuration Data) Issues

1. Create a bootable usb drive
2. Go to "Repair your computer" in the installation window
3. Go to "Command Prompt"

```
bcdedit
```

`bootrec` stands for boot recovery.

`bootrec /?` shows what entries we've got.

`bootrec /rebuildbcd`

# Resolving a Hard Drive Related Boot Issue

# `bootrec /fixboot` "Access is denied."

`diskpart`

To list all the disks, type:

`list disk`

`select disk 0` (or `select disk #`)

To list all the volumes, type:

`list vol`

Then select the volume where the system is:

`select vol 0` (or `select vol #`)

Assign it with a letter not in use:

`assign letter=V:` (or `assign letter=OTHER_CHAR:`)

`exit`

Change directory to volume V:

`V:`

`md \efi\microsoft\boot\`

# Another Way

`diskpart`

`select disk 0`

`list partition`

`select partition X`  (X is the partition number where Windows is installed)

If not fixed mbr, then type:

`clean`

`convert mbr`

`create partition primary size=300000`

After that, continue with:

`active`

`exit`

`bcdboot C:\windows` (if C is your windows partition)
