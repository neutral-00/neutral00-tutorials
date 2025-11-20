# Create Ubuntu VM

Create a Virtual Machine With Ubuntu as the OS.

> Refer this blog: https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview

<section>
- Run VirtualBox
- *Create a new virtual machine*
	- Click Machine>New
	- Fill the details
		- name: ubuntu
		- folder: D:\Program Data\VirtualBox VMs
		- ISO image: C:\Users\user-name\Downloads\ubuntu-xx.xx.x-desktop-amd64.iso
	- Click Next
	- Change the username and password to create user without sudo access.
		- username: linuxuser00
		- password: Lxxxxxx_00
		- hostname: ubuntu
		- domainname: myguest.virtualbox.org
		- guest additions | checked
		- install in background | leave unchecked
	- If you use default, user will be created without sudo access.
	- Click Next
	- Virtual Machine’s resources
		- For good performance it’s recommended to provide your VM with around 8GB of RAM (althought 4GB will still be usable) and 4 CPUs
		- Try to remain in the green areas of each slider to prevent issues with your machine
		- base memory: 8192
		- processors: 8
	- Click Next
	- Set the virtual harddisk.
		- For Ubuntu recommended around 25 GB as a minimum.
		- I have given 50 GB
		- By default the hard disk will scale dynamically as more memory is required up to the defined limit.
	- Click Next
	- Review the details
		- host/domain name is: ubuntu.myguest.virtualbox.org
	- Click Finish
	- Install Image
		- Click Start to launch the virtual machine.
		- You will see a message saying ‘Powering VM up …’ and your desktop window will appear
		- On first boot the unattended installation will kick in so do not interact with the prompt
		- let it progress automatically to the splash screen and into the installer
		- If you chose not to use unattended install then you will need to progress through the Ubuntu install manually.
			- you checkout the installation guide here: https://ubuntu.com/tutorials/install-ubuntu-desktop#4-boot-from-usb-flash-drive
		- You will notice at this stage that the resolution of the window is fixed at 800x600. 
		- This is because the Guest Additions features are not installed until after the Ubuntu installation has completed.
		- Once the installation completes, the machine will automatically reboot to complete the installation.
		- Finally you will be greeted with the Ubuntu log-in screen where you can enter your username and password defined during the initial setup
	- Enjoy your shiny new Ubuntu Desktop!
</section>