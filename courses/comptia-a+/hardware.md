## Network cables

- Copper wires in Ethernet cables have twists to reduce interference
- Coaxial cables
- Plenum-rated cable
- Unshielded and shielded cables
  - (Overall cable) / (individual pairs)TP eg. S/FTP

## Optical Fiber

- Multimode fiber : up to 2km , LED (cheaper)
- Singlemode fiber : up to 100km , lasers (expensive)

## Cables

- SATA data port (7 pin)
- SATA power port (15 pin)
- eSATA cable

## Others

- T568A and T568B are standards for wiring twisted pair network cables, including Ethernet cables
- SCSI (communication standard like SATA)
- SAS (Serial Attached SCSI)
- daisy chain : wiring scheme , wire together in a ring
- SATA (Serial-ATA (Advanced Technology Attachment) )
- PATA (Parallel-ATA)
- PCIe
- BIOS (Basic Input/Output System)
- UEFI BIOS replace legacy BIOS (a standardization for BIOS)
- Reset BIOS : 1. CMOS Battery(remove and put back) 2.Clear CMOS Jumper(short 2 pins)
- CPU: "32-bit" and "64-bit" refer to CPU architecture , CORES , MULTITHREADING , VIRTUALIZATION SUPPORT
- DSL (Digital Subscriber Line) is a technology used to provide high-speed internet access over traditional telephone lines
- ECC (Error Correcting Code) Memory
- RAM parity (even parity check)
- M.2 interface
- AHCI vs NVMe

## Connectors

- RJ11 (DSL)
- RJ45 (ethernet)
- F-connecter(for coaxial cable)
- Molex connector (eg.computer PSU)

## Power

PSU converts incoming electrical power (usually from an outlet) to the appropriate voltage required by the devices it powers

## RAID

- Stands for **Redundant Array of Independant Disks**

### RAID 0 - Striping

- Data is striped across 2 disks
- Not fault tolerant
- For speed

### RAID 1 - Mirroring

- Data is mirrored across 2 disks

### RAID 5 - Striping with parity

- Needs 3 or more disks
- Data is rebuilt when a disk fails

### RAID 10(1+0, or Mirroring + Striping)

- Combines RAID 1 and RAID 0 by mirroring pairs of drives and then striping data across these mirrored pairs.

### RAID Summary

| RAID Level | Minimum Drives | Usable Space Formula                            | Fault Tolerance           |
| ---------- | -------------- | ----------------------------------------------- | ------------------------- |
| RAID 0     | 2              | Number of Drives x Size of Smallest Drive       | No fault tolerance        |
| RAID 1     | 2              | Size of One Drive                               | 1 drive                   |
| RAID 5     | 3              | (Number of Drives - 1) x Size of Smallest Drive | 1 drive                   |
| RAID 10    | 4              | (Number of Drives / 2) x Size of Smallest Drive | 1 drive per mirrored pair |
