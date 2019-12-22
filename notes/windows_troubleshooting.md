# Windows Troubleshooting

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
