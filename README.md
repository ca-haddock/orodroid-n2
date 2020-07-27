# orodroid-n2

Arch Linux ODROID-N2 Mainline Kernel

Zur Installation des Mainline Linux Kernel sind lediglich zwei Schritte notwendig: Aktualisierung der boot.ini, Installation des Mainline Kernel und Deinstallation des odroid Kernels. Zunächst wird die boot.ini aktualisiert. Die Datei liegt im Ordner /boot/ und bekommt folgenden Inhalt:
Inhalt der boot.ini für Mainline Kernel
```
ODROIDN2-UBOOT-CONFIG
setenv bootlabel "ArchLinux EMMC"

# Default Console Device Setting
setenv condev "console=ttyAML0,115200n8 console=tty1"   # on both

# Boot Args
setenv bootargs "root=/dev/mmcblk${devno}p2 rootwait rw ${condev} ${amlogic} no_console_suspend fsck.repair=yes net.ifnames=0 hdmimode=1080p60hz clk_ignore_unused"

# Set load addresses
setenv dtb_loadaddr "0x20000000"
setenv loadaddr "0x1080000"
setenv initrd_loadaddr "0x3080000"

# Load kernel, dtb and initrd
load mmc ${devno}:1 ${loadaddr} /Image
load mmc ${devno}:1 ${dtb_loadaddr} /dtbs/amlogic/meson-g12b-odroid-n2.dtb
load mmc ${devno}:1 ${initrd_loadaddr} /initramfs-linux.uimg
#fdt addr ${dtb_loadaddr}

# boot
booti ${loadaddr} ${initrd_loadaddr} ${dtb_loadaddr}
```

Anschließend kann der Mainline Kernel von ArchLinux ARM oder einer beliebigen Quelle installiert werden.
Im Beispiel wird das Aarch64 Paket gewählt, also ein 64bit System.
Installation Mainline Linux Kernel auf ODROID N2

$ pacman -S linux-aarch64

