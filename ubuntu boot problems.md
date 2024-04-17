# ubuntu boot problems

## ubuntu destroys / deletes the windows boot loader

### solving problem using boot repair
boot a light ubuntu system on pc and then:
- install boot repair from these documentation: <a href="https://askubuntu.com/questions/217904/unable-to-boot-into-windows-after-installing-ubuntu-how-to-fix">askubuntu question</a>
- run boot repair
- go to Advanced Options -> Other Options tab -> Repair Windows boot files.
- The boot flag should be placed on the same partition on which Ubuntu is installed
- The partition on which Ubuntu is installed can be identified from the Disks application which is built-in in Ubuntu
- If you're unable to select the Repair Windows boot files option because it's grayed out
    - `sudo add-apt-repository ppa:yannubuntu/boot-repair <br/>
        sudo apt-get update <br/>
        sudo apt-get install -y boot-repair<br/>
        sudo boot-repair`
    - Open the Boot Repair application, try the recommended repair first, then restart
    -  If Windows still doesn't show in the Grub menu, boot into Ubuntu and open Boot Repair again
    - click advanced options, and in the second tab from the left (Grub location), select the dropdown menu for the option: OS to boot by default and select Windows (via the sda5 menu)
    - Restart the computer. In the grub menu, to boot by Windows, quickly tap down to go to Windows and press enter, making sure you cancel the 5 s timeout by tapping down, before the 5 s timeout automatically selects the option highlighted.


### solving problem using Rescatux
Rescatux is a free bootable live CD/USB that can repair GRUB and the Windows bootloader. Rescatux has a graphical interface with a menu of operating system rescue tasks. If your hard disk has the MBR partitioning format, you can select the Restore Windows MBR (BETA) option to repair the Windows bootloader. If your computer has UEFI firmware, you can select among the UEFI boot options.

### expert tools
- boot repair
- GParted
- OS-Uninstaller
- Clean-Ubiquity
- PhotoRec
- TestDisk

# Alternative options

Create a file, /boot/grub/custom.cfg (by running sudo -H gedit /boot/grub/custom.cfg) with these contents: <br/>

```
#This entry should work for any version of Windows installed for UEFI booting

menuentry "Windows (UEFI)" {
 search --set=root --file /EFI/Microsoft/Boot/bootmgfw.efi
 chainloader /EFI/Microsoft/Boot/bootmgfw.efi
}
```

