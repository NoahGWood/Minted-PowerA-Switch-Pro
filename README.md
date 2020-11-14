# Minted-PowerA-Switch-Pro
Instructions on setting up the Nintendo Switch Pro controller from PowerA on Linux Mint

## Steps
1. Steam Controller Installation
  > sudo apt-get install steam-devices
2. Set-up udev rules
  > sudo nano /lib/udev/rules.d/99-steam-controller-perms.rules
  > Copy & paste the following:
  # Nintendo Switch Pro Controller over USB hidraw
  KERNEL=="hidraw*", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="2009", MODE="0666"
  # PowerA model
  KERNEL=="hidraw*" ATTRS{idVendor}=="20d6", ATTRS{idProduct}=="a711", MODE="0666"

  # Nintendo Switch Pro Controller over bluetooth hidraw
  KERNEL=="hidraw*", KERNELS=="*057E:2009*", MODE="0666"
  # Power A Model
  KERNEL=="hidraw*", KERNELS=="*20d6:a711", MODE="0666"
  
## Troubleshooting
If this isn't working with your controller, you might have another brand or model, an easy solution is to try replacing the vendor id and product id, to find this information, perform the following

1. Unplug controller (if plugged in)
2. Open a terminal (Ctrl+T) and type "dmesg" - DO NOT HIT ENTER
3. Plug in controller
4. Hit enter

You should now see something like this:
[ 3105.852718] usb 3-3: new full-speed USB device number 14 using xhci_hcd
[ 3106.008663] usb 3-3: New USB device found, idVendor=20d6, idProduct=a711, bcdDevice= 2.00
[ 3106.008665] usb 3-3: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 3106.008667] usb 3-3: Product: Core (Plus) Wired Controller
[ 3106.008668] usb 3-3: Manufacturer: Bensussen Deutsch & Associates,Inc.(BDA)
[ 3106.008669] usb 3-3: SerialNumber: 000000000001
[ 3106.031116] input: Bensussen Deutsch & Associates,Inc.(BDA) Core (Plus) Wired Controller as /devices/pci0000:00/0000:00:07.1/0000:09:00.3/usb3/3-3/3-3:1.0/0003:20D6:A711.000F/input/input38
[ 3106.031291] hid-generic 0003:20D6:A711.000F: input,hidraw4: USB HID v1.11 Gamepad [Bensussen Deutsch & Associates,Inc.(BDA) Core (Plus) Wired Controller] on usb-0000:09:00.3-3/input0

Search for the idVendor and idProduct, these numbers you will use in the udev rules.

In your updated udev rules add the following lines:

# [Some description of your controller]
KERNEL=="hidraw*", ATTRS{idVendor}=="REPLACE_WITH_IDVENDOR", ATTRS{idProduct}=="REPLACE_WITH_IDPRODUCT", MODE="0666"

# [Some description of your controller]
KERNEL=="hidraw*", KERNELS="REPLACE_WITH_IDVENDOR:REPLACE_WITH_IDPRODUCT", MODE="0666"
