# MinisForum N300 ACPI Bug
MinisForum N300 ACPI Bug - Tested on Debian 12.5, Fedora 40.

dmesg output: 

```
[    0.476146] ACPI BIOS Error (bug): Could not resolve symbol [\_SB.UBTC.RUCC], AE_NOT_FOUND (20230628/psargs-330)
[    0.476156] ACPI Error: Aborting method \_SB.PC00.TXHC.RHUB.SS01._PLD due to previous error (AE_NOT_FOUND) (20230628/psparse-529)
[    0.476202] ACPI BIOS Error (bug): Could not resolve symbol [\_SB.UBTC.RUCC], AE_NOT_FOUND (20230628/psargs-330)
[    0.476206] ACPI Error: Aborting method \_SB.PC00.TXHC.RHUB.SS02._PLD due to previous error (AE_NOT_FOUND) (20230628/psparse-529)
```

```
[    5.672602] ACPI BIOS Error (bug): Could not resolve symbol [\_SB.UBTC.RUCC], AE_NOT_FOUND (20230628/psargs-330)
[    5.672605] ACPI Error: Aborting method \_SB.PC00.TXHC.RHUB.SS01._PLD due to previous error (AE_NOT_FOUND) (20230628/psparse-529)
[    5.672615] ACPI BIOS Error (bug): Could not resolve symbol [\_SB.UBTC.RUCC], AE_NOT_FOUND (20230628/psargs-330)
[    5.672616] ACPI Error: Aborting method \_SB.PC00.TXHC.RHUB.SS01._PLD due to previous error (AE_NOT_FOUND) (20230628/psparse-529)
```
```
[    6.506370] ACPI BIOS Error (bug): Could not resolve symbol [\_SB.UBTC.RUCC], AE_NOT_FOUND (20230628/psargs-330)
[    6.506380] ACPI Error: Aborting method \_SB.PC00.TXHC.RHUB.SS01._PLD due to previous error (AE_NOT_FOUND) (20230628/psparse-529)
[    6.507758] ACPI BIOS Error (bug): Could not resolve symbol [\_SB.UBTC.RUCC], AE_NOT_FOUND (20230628/psargs-330)
[    6.507768] ACPI Error: Aborting method \_SB.PC00.TXHC.RHUB.SS01._PLD due to previous error (AE_NOT_FOUND) (20230628/psparse-529)
```
chroot sequence (Live Fedora 40):

```
cd /
sudo mount -t ext4 /dev/sdx (sda1 on test system) /mnt
sudo mount -t proc proc /mnt/proc
sudo mount -t sysfs sys /mnt/sys
sudo mount -o bind /dev /mnt/dev
sudo mount --bind /run /mnt/run

If network is down:
sudo cp -L /etc/resolv.conf /mnt/etc/resolv.conf

chroot:
sudo chroot /mnt /bin/bash

Unable to allocate pty: No such device
Option 1: sudo mount --rbind /dev/ /mnt/dev/
Option 2: sudo mount --bind /dev/pts/ /mnt/dev/pts/

exit

sudo umount /mnt/run
sudo umount /mnt/{proc,sys,dev}

sudo umount /mnt

reboot
```

Debian Testing Mirrors:

```
deb [arch=amd64] http://cdn-fastly.deb.debian.org/debian/ testing main contrib non-free
deb-src [arch=amd64] http://cdn-fastly.deb.debian.org/debian/ testing main contrib non-free

deb [arch=amd64] http://cdn-fastly.deb.debian.org/debian/ testing-updates main contrib non-free
deb-src [arch=amd64] http://cdn-fastly.deb.debian.org/debian/ testing-updates main contrib non-free
```

- [Intel® Core™ i3-N300 Processor](https://ark.intel.com/content/www/us/en/ark/products/231806/intel-core-i3-n300-processor-6m-cache-up-to-3-80-ghz.html)
- [MINISFORUM Mini PC UN300 8GB LPDDR5 256GB SSD with Intel Core i3-N300 (Amazon)](https://www.amazon.com/MINISFORUM-LPDDR5-i3-N300-Business-Computer/dp/B0CQYSRDLV)
- [MINISFORUM Venus Series UN300 Mini PC Core i3 (Walmart)](https://www.walmart.com/ip/MINISFORUM-Venus-Series-UN300-Mini-PC-Core-i3-N300-up-3-8GHz-Windows-11-Home-8GB-RAM-256GB-SSD-2xHDMI-1xUSB-C-4K-60Hz-Triple-Outputs-2xRJ45-Port-4xUS/5516005036)
