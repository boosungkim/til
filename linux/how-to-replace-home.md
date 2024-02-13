# How to handle a space in the section title

The other day, my home partition got corrupted. Thankfully, my home and root directories are on separate partitions. Here is how to replace just the home partition with the KDE partition manager.

## Decrypt drive
Boot into a live CD.

```bash
lsblk
sudo cryptsetup luksOpen /dev/sdX myvolume
```
Don't forget to close cryptsetup when you are done!

## Extract data
Mount external drive for back up.

```bash
sudo apt install testdisk
sudo testdisk
```

## Shred and replace
Shred the old home partition and create a new one via KDE partition manager. Set the correct format and label.

Confirm correct /etc/fstab entry via `sudo cat /etc/fstab`.

Reboot and enter system recovery mode through GRUB.

If default home directories and files are not created, use `/etc/skel` or `xdg-user-dirs`.

### `/etc/skel`
This copies the default configuration files from the system-wide default user settings.

```bash
su - username
sudo cp /etc/skel/.* /home/user
```

### `xdg-user-dirs`
This tool is used by Debian to automatically create default home directories.

```bash
su - username
sudo apt install xdg-user-dirs
xdg-user-dirs-update
```

### Set ownership and permissions
```bash
sudo chown -R user:user /home/user
chmod -R 755 /home/user
```

Reboot, and everything should work!