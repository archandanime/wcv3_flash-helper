## wcv3_flash-helper - Automatic partition backup/restore tool for Wyze Cam v3

## Feature list
- No serial connection or SSH is required, only with SD card.
- Custom filenames for backup/restore.
- Custom script to run after backup/restore.
- Dry run option for safety and debugging.
- Seamless transition to a new boot image on SD card after backup/restore.
- Initramfs shell is available if you have a serial connection.

## How to backup your partitions - Read this if this is your first use
1. Download [lastest release](https://github.com/archandanime/wcv3_flash-helper/releases/latest) then extract the `wcv3_flash-helper` directory and `factory_t31_ZMC6tiIDQN` to your SD card.
2. Edit the config file `wcv3_flash-helper.conf` with:
```
dry_run="yes"
backup_partitions="yes"
restore_partitions="no"custom_script=""
```
3. Insert your SD card and power on your camera.
4. Wait for the camera to restart after wcv3_flasher-helper finishes its operations. Then turn the off camera, remove your SD card, and check `wcv3_flash-helper.log` on your SD card to see if everything looks fine and there is no error.
5. Edit `wcv3_flash-helper.conf` same as Step 1, but with the `dry_run` option turned off.
6. Do Steps 3 and 4 again, then check your SD card, there should be a `wcv3_flash-helper_backup` directory where backups of your partitions are stored. Copy it to a safe place in case you need it for recovery.

## How to restore partitions
1. Download [lastest release](https://github.com/archandanime/wcv3_flash-helper/releases/latest) then extract the `wcv3_flash-helper` directory and `factory_t31_ZMC6tiIDQN` to your SD card.
2. Edit `wcv3_flash-helper.conf` with the filenames of the partition images used for backup/restore.
3. Edit `wcv3_flash-helper.conf` to select partitions to be restored.
4. Insert your SD card into your camera and reboot.

## Run a custom script
You can write a script and specify it in the `wcv3_flash-helper.conf` file with the `custom_script` option. This script will be executed after backup/restore operations are finished. This is useful if you want to flash custom partitions and write your configuration files to the `configs` partition.

## Specify the boot image on the SD card that will be used on the next boot
If you are using wz_mini_hacks, you can rename wz_mini's boot image to `factory_t31_ZMC6tiIDQN.wz_mini` and specify that file name with the `continue_boot_img_filename` option. After wcv3_flash-helper finishes its operations, this file will be renamed to `factory_t31_ZMC6tiIDQN` to allow this boot image to be booted on the next boot without having to pull the SD card and rename it manually. Seamless transition!

**Notes:**
- You need md5sum files of the partition images that you want to restore in `<restore_partition>.ms5sum` format. Backup operations will automatically generate md5sum files.
- It is highly recommended to enable `dry_run` to check if everything works before doing real operations.
- Backup is done first, then Restore and followed by Custom script.
- Custom script is not run if `dry_run` is set to `yes`.
- Custom script does not necessarily have to be on the SD Card top directory, you can put its path on the option to make it run from somewhere else.
- During backup operations, the blue LED would be blinking. During restore operations, the red LED would be blinking.

## Warning
```
I am not responsible for bricking someone's camera.
Though it has been tested carefully, the bootloader partition won't ever be touched.
It is still possible to hardbrick the camera with your custom script or command injection in the config file.
Dry run first is highly recommended, unless you are confident.
```

## Credits
- Gtxaspec with his full-featured busybox from [his repo](https://github.com/gtxaspec/wz_mini_hacks)
- Mnakada with their docker image to build the boot image from [their repo](https://github.com/mnakada/atomcam_tools)
