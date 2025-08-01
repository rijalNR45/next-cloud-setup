# next-cloud-setup
This is my personal documentation of next-cloud setup in my ubuntu.
This is a personal project and will act as a future reference for me. This is **NOT** a tutorial. I suggest to lookup at the official next cloud documentation if you also want to try something like this. I am using dell latitude 3470 with intel core i3-6100U. The RAM is of 4GB and SSD of 256GB. 

# 1. Updating the system
At first, we are going to make sure that we have all the latest softwares updated on our ubuntu 24.04.2 LTS. We simply run this code to do so. 

sudo apt update && sudo apt upgrade -y

# 2. Snap package manager installed or not?
Then, we check if snap package is instaled or not by 
snap --version
if available, it will display the version, else it says command not found.
If not, just install it using this command:

sudo apt install snapd -y

# 3. Install next cloud

Installing next cloud is super simple thanks to snap which handles 10+ manual configurations all by itself. It configures databases, php and web servers automatically. Just running this command, next cloud will be installed!

sudo snap install nextcloud
 Check if installed or not:

 sudo nextcloud.occ --version
 
# 4. Check information of next cloud
Now, we have to check if next cloud is functioning properly or not. Run a simple command:

sudo snap services nextcloud
snap info nextcloud

Now create your id with:

sudo nextcloud.manual-install yourusername yourpassword

It will output as: Nextcloud was successfully installed

# 5. Check ports 
Next cloud could run in two ports: for http and https. Check the ports by this command.

sudo snap get nextcloud ports

You will get key value pair for http and https ports.

# 6. Check ports availability

Sometimes, services like apache2 might be blocking port 80. Check if thats the case by:

sudo netstat -tlnp | grep :80

If you see something like this:

tcp6       0      0 :::80                   :::*                    LISTEN      1379/apache2

then you need to stop and disable apache2 or any other service that might override the port. Simply do:

sudo systemctl stop apache2
sudo systemctl disable apache2

Now you can restart nextcloud by:

sudo snap restart nextcloud
 now, we need to find ip address of our device. To do that simply:

 ip addr show | grep inet

 The ip with format 192.168.1.__ is mostly our ip.

 That ip should be added to trusted domains with:

 sudo nextcloud.occ config:system:set trusted_domains 1 --value=192.168.1.__

 # open firewall for phone access

 to access from phone, open firewall with this command:

 sudo ufw allow 80

# work in phone

now install the app or browse the official next cloud website from your phone. Enter the ip address for the host i.e. 192.168.1.__ . Then enter your login credentials to gain access to the cloud!


 


