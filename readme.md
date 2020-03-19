Steps described below are taken from https://askubuntu.com/questions/364972/realtek-8188cus-doesnt-work/395340#395340.

These solutions are from an answer by [SirCharlo](https://askubuntu.com/users/40421/sircharlo).



First of all, ensure you have the necessary prerequisites:

`sudo apt-get install linux-headers-generic build-essential dkms git`

Clone the updated driver with git:

`git clone https://github.com/pvaret/rtl8192cu-fixes.git`

Set it up as a DKMS module:

`sudo dkms add ./rtl8192cu-fixes`

Build and install the driver, you may need check the version here (e.g. 1.9 may change):

`sudo dkms install 8192cu/1.9`

Refresh the module list:

`sudo depmod -a`

Ensure the native (and broken) kernel driver is blacklisted:

`sudo cp ./rtl8192cu-fixes/blacklist-native-rtl8192.conf /etc/modprobe.d/`

Let's not take any chances. Instruct Ubuntu to load the new driver when it starts up.

`echo 8192cu | sudo tee -a /etc/modules`

Reboot.
You're done.