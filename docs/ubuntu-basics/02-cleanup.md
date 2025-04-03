# Cleanup Ubuntu

**Cleaning up unnecessary files in Ubuntu**

To clean up unnecessary files in Ubuntu, you can use the following methods:

1. **Remove cache files**:
   - Open the terminal and run the command: `sudo apt autoremove`
   - This will remove any unnecessary packages and their dependencies.
   - Additionally, run the command: `sudo apt autoclean` to remove any cached packages.

2. **Remove logs**:
   - Open the terminal and run the command: `sudo rm -rf /var/log/*`
   - This will remove all log files in the `/var/log` directory.

3. **Remove temporary files**:
   - Open the terminal and run the command: `sudo rm -rf /tmp/*`
   - This will remove all files in the `/tmp` directory.

4. **Remove unnecessary packages**:
   - Open the terminal and run the command: `sudo apt list --installed | grep -i "unwanted"`
   - Replace "unwanted" with the name of the package you want to remove.
   - To remove the package, run the command: `sudo apt remove <package_name>`

5. **Use the `du` command to find large files**:
   - Open the terminal and run the command: `sudo du -h / | sort -h`
   - This will list all directories and their sizes in a human-readable format.
   - You can then use the `rm` command to remove the large files.

6. **Use the `cleanmgr` command to clean up disk space**:
   - Open the terminal and run the command: `sudo cleanmgr`
   - This will start the disk cleanup process.

7. **Use the `Disk Cleanup` tool**:
   - Open the Files application and navigate to the **Other Locations** section.
   - Click on the **Trash** and **System** folders to clean up any unnecessary files.

**Remember to be careful when deleting files, as some files may be essential for your system to function properly.**

sudo apt-get autoremove will remove unneeded packages and config files, and sudo apt-get autoclean will remove incompletely installed packages, sudo apt-get clean will clear the apt-get cache. 

You can also regain space by uninstalling localisation files you don't need. Use a script named localepurge for this
sudo apt-get install localepurge
sudo localepurge
