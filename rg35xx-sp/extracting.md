# Extracting

## Firmware & Bootloader

### Get the OFW

Simply download it from Anbernic's [official website](https://win.anbernic.com/download/412.html) and then extract the 16GB version from the zip.

```bash
mv RG35XXSP-V1.0.3-EN16GB-240511.IMG RG35XXSP_OFW.img
```

### Extract boot0.img

```bash
dd if=RG35XXSP_OFW.img of=boot0.img bs=1024 skip=8 count=64
```

### Extract boot\_package.img

```bash
dd if=RG35XXSP_OFW.im of=boot_package.img bs=1024 skip=16400 count=20464
```

### Extract \`boot.img\` & \`env.img\`

```bash
fdisk -l path/to/RG35XXSP_OFW.img #Linux
```

```bash
hdiutil imageinfo RG35XXSP_OFW.img #MacOS
```

