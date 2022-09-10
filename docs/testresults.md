Functionality
==========
The dietSCSI has been tested for at least basic functionality on the following computers/devices:

| Device                                             | OS                                     | Result |
|----------------------------------------------------|----------------------------------------|--------|
| Macintosh Classic II                               | System 7.1.2, System 7.5.5             | Works  |
| Macintosh Performa 630CD                           | System 7.5.5, Mac OS 8.1               | Works  |
| Power Macintosh G4 with Adaptec 2906 PCI SCSI card | Mac OS 9.2.2, Mac OS 10.4, Mac OS 10.5 | Works  |
| Generic Pentium PC with HP 53C416 ISA SCSI card    | Windows 98                             | Works  |


Performance
==========
All testing was done on a Macintosh Performa 630CD using firmware 1.1-SNAPSHOT-20220107.  Data was gathered using TimeDrive 2.0.3.

| SD_Card                      | Card_Format | MCU      | OS           | Latency  | Average_Seek | Max_Seek   | Write     | Read      |
|------------------------------|-------------|----------|--------------|----------|--------------|------------|-----------|-----------|
| Gigastone High Endurance 8GB | exFAT       | GD32F103 | System 7.5.5 | 2.714 ms | 26.136 ms    | 75.190 ms  | 1169 KB/s | 1160 KB/s |
| Gigastone High Endurance 8GB | exFAT       | GD32F103 | Mac OS 8.1   | 2.633 ms | 25.244 ms    | 75.333 ms  | 1162 KB/s | 1159 KB/s |
| Patriot 32GB                 | exFAT       | GD32F103 | System 7.5.5 | 2.639 ms | 25.657 ms    | 75.232 ms  | 1160 KB/s | 1161 KB/s |
| Gigastone High Endurance 8GB | exFAT       | HK32F103 | System 7.5.5 | 3.318 ms | 40.315 ms    | 115.728 ms | 859 KB/s  | 917 KB/s  |
| Patriot 32GB                 | exFAT       | HK32F103 | System 7.5.5 | 3.240 ms | 39.864 ms    | 115.836 ms | 856 KB/s  | 918 KB/s  |
