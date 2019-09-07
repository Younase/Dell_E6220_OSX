
Install Osx using /r/Hackintosh guide (you can install mojave by installing High Sierra, patching mojave, then installing it )
# Install clover on your main disk:
start clover, follow steps, choose your main drive, let it install.
mount the EFI partition on your main disk using clover configurator (or do it manually by following the 4 first steps):
1. sudo -s
2. diskutil list 
3. mkdir /Volumes/EFI
4. mount_msdos /dev/diskXsX /Volume/EFI
copy your EFI folder from the USB stick to the newly mounted volume
5. umount -f /dev/diskXsX
6. rm -rf /Volumes/EFI
restart laptop, go to bios options, select UEFI add new choose a name, path EFI/BOOT/Cloverx64.efi 
change default disk in config.plist to the disk you want to start by default

# OPTIONAL:
## SSDT patch for more cpu temp/power states (return n on execution):
cd ~
curl -o ./ssdtPRGen.sh https://raw.githubusercontent.com/Piker-Alpha/ssdtPRGen.sh/master/ssdtPRGen.sh
chmod +x ./ssdtPRGen.sh
./ssdtPRGen.sh
cp ~/Library/ssdtPRGen/ssdt.aml /Volumes/EFI/EFI/Clover/ACPI/patched/SSDT.aml

## FakeSMC sensor map:
SMM -> Fan
ACPI -> ambient 
