## Getting info

> Ref. https://forum.odroid.com/viewtopic.php?t=19419

```bash
# dmesg | grep -i touch
[ 421.337993] hid-generic 0003:0EEF:0005.0003: hiddev0: USB HID v1.10 Device [RPI_TOUCH By ZH851] on usb-dwc2_a-1/input0
```
Dmesg sees the devive as hiddev0

```bash
# lsusb
Bus 001 Device 002: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 004: ID 0eef:0005 D-WAV Scientific Co., Ltd
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

lsusb sees the D-Wav device

## Testing the touch

```bash
# xxd -c 25 /dev/usb/hiddev0
00000000: 0300 8c00 aa00 0000 0300 8c00 0000 0000 0300 8c00 0000 0000 03 .........................
00000019: 008c 0000 0000 0003 008c 0000 0000 0003 008c 0000 0000 0003 00 .........................
00000032: 8c00 bb00 0000 0300 8c00 0100 0000 0300 8c00 0000 0000 0300 8c .........................
0000004b: 0000 0000 0003 008c 0000 0000 0003 008c 0000 0000 0003 008c 00 .........................
00000064: 0000 0000 0300 8c00 0000 0000 0300 8c00 0000 0000 0300 8c00 00 .........................
0000007d: 0000 0003 008c 0000 0000 0003 008c 0000 0000 0003 008c 0000 00 .........................
```

Using xxd command on hiddev0 spits out lots of data, BUT ONLY WHEN TOUCH..and stops immediately when you pull your finger away

