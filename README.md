## wcv3_flash-helper - Automatic parttion backup/restore tool for Wyze Cam v3

## Feature list
- No serial connection or SSH is required, only with SD Card
- Custom filenames for backup/restore
- Custom script to run after backup/restore
- Dry run option for safety and debugging
- Seamless transition to new boot image on SD Card after backup/restore
- Initramfs shell is available if you have serial connection

## Read this if this is your first time
1. Download [lastest release](https://github.com/archandanime/wcv3_flash-helper/releases) and extract `wcv3_flash-helper` directory and `factory_t31_ZMC6tiIDQN` to your SD Card.
2. Edit the config file `wcv3_flash-helper.conf` with:
```
dry_run="yes"
backup_partitions="yes"
restore_partitions="no"
custom_script=""
```
3. Insert your SD Card and power on your camera.
4. Wait until the camera restart, turn it off, remove your SD Card and check `wcv3_flash-helper.log` if everything looks fine and there is no error.
5. Edit `wcv3_flash-helper.conf` same as Step 1 but with `dry_run` option turned off.
6. Do Step 3 and 4, check your SD Card, there should be `wcv3_flash-helper_backup` directory. Copy it to a safe place in case you need for a recovery.

## Normal installation
1. Download [lastest release](https://github.com/archandanime/wcv3_flash-helper/releases) and extract `wcv3_flash-helper` directory and and `factory_t31_ZMC6tiIDQN` to your SD Card.
2. Edit `wcv3_flash-helper.conf` with filenames of the partition images.
3. Edit `wcv3_flash-helper.conf` to select partitions to be restored.
4. Insert your SD Card to your camera and reboot.

**Notes:**
- You need md5sum files of the partition images that you want to restore in `<restore_partition>.ms5sum` format. Backup operations will automatically generate md5sum files.
- It is highly recommended to enable `dry_run` to check if everything works before doing real operations.
- Backup is done first, then Restore and followed by Custom script.
- Custom script is not run if `dry_run` is set to `yes`.
- You can specify `continue_boot_img_filename` option with a boot image to be booted on next boot, It will be renamed to `factory_t31_ZMC6tiIDQN` after all operations are finished.
- Custom script does not neccessarily have to be on SD Card top directory, you can put its path on the option to make it run from somewhere else.
- During backup operations, blue LED would be blinking. During restore operations, red LED would be blinking.

## Warning
```
I am not resposible for bricking someone's camera.
Though it has been tested carefully and bootloader partition won't ever be touched.
It is still possible to hard brick the camera with your custom script or command injection on the config file.
Dry run first is highly recommended, unless you are confident.
```

## Credits
- Gtxaspec with his full-featured busybox from [his repo](https://github.com/gtxaspec/wz_mini_hacks)
- Mnakada with their docker image to build the boot image from [their repo](https://github.com/mnakada/atomcam_tools)
