# A modified grub allowing tweaking hidden BIOS settings.
based on grub with [setup_var patch (invalid link now)](http://luna.vmars.tuwien.ac.at/~froemel/insydeh2o_efi/grub2-add-setup_var-cmd.patch) and [setup_var2 patch](https://habr.com/post/190354/).

What does this fork do differently? Instead of modifying the Setup variable, I have modified it to read AmdSetup instead for AMD CBS configurations. setup_var and setup_var2 does something different now. Setup_var works as expected except it accesses AmdSetup instead, and setup_var2 will print all variables, and you can press enter to print the next one. 

Looking for the version that modifies 'Setup' instead? See here: https://github.com/datasone/grub-mod-setup_var
## The problem
Most laptop manufactures lock down their BIOSes very securely with RSA signing nowadays. This bypasses the dillema of finding a bypass to flash a modified BIOS and instead modifies the NVRAM registers instead.

USE WITH CAUTION AND ENSURE YOU HAVE EXAMINED YOU ARE ACCESSING RIGHT SETUP VARIABLE OR YOU WILL RISK BRICKING YOUR COMPUTER!!! I AM NOT RESPONSIBLE IF ANYTHING HAPPENS TO YOUR COMPUTER, INCLUDING BUT NOT LIMITED TO: SPONTANEOUS COMBUSTION, IMPLOSION, THERMONUCLEAR MELTDOWN. YOU HAVE BEEN FOREWARNED!

Okay in most cases you can recover by removing the CMOS battery or reflashing the eeprom with a programmer no matter how messed up your nvram is. BUT NO PROMISES. 

## Build Notes
Grub has been updated to the latest release and the newest gcc does indeed compile if you run ```./configure --prefix=$HOME/local --with-platform=efi --disable-werror```. Note the --disable-werror.

Build:

```
./autogen.sh
./configure --prefix=$HOME/local --with-platform=efi --disable-werror
make
make install

```

Generating modified GRUB shell:
```
cd $HOME/local
./bin/grub-mkstandalone -O x86_64-efi -o modGRUBShell.efi

```

