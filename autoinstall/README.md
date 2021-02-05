# Autoinstall
By using autoinstall we could automate the installer like what `presed` is used for `d-i`.

## Usage
1. Upload your `user-data` to a www server. You may use `basic.yaml` as an example. Rename `basic.yaml` and put it 
   into a www server to serve it.
2. `touch <your www server>/meta-data` to create an empty but necessary file required by `cloud-init`.
3. Edit `grub.cfg` to include the necessary kernel parameters `autoinstall "ds=nocloud-net;s=http://<www-server-url>/"`. For example,
     - as is `linux   /casper/vmlinuz    quiet splash root=/dev/ram0 ramdisk_size=1500000 ip=dhcp url=http://<server-provides-image>/focal-live-server-arm64.iso ---`
     - to be `linux   /casper/vmlinuz    quiet splash root=/dev/ram0 ramdisk_size=1500000 ip=dhcp url=http://<server-provides-image>/focal-live-server-arm64.iso autoinstall "ds=nocloud-net;s=http://<server-provides-user-data>/" ---`

## Trouble-shooting and Tips
- The format of the first line "shebang", a.k.a. `#cloud-config` matters. Do not change it or input extra spaces 
  unless you know what you are doing.
- The double quotes matters when injecting user-data in the kernel parameters of Grub2 menu.
- The trailing of the url serving `user-data` matters in the current autoinstall version.