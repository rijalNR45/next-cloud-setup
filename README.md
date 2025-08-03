# next-cloud-setup
This is my personal documentation of next-cloud setup in my ubuntu.
This is a personal project and will act as a future reference for me. This is **NOT** a tutorial and I won't be responsible if anything goes wrong if you decide to follow these steps. I suggest to lookup at the official [nextcloud documentation](https://docs.nextcloud.com/)  if you also want to try something like this. I am using Dell Latitude 3470 with intel core i3-6100U. The RAM is of 4GB and SSD of 256GB. 

# 1. Updating the system
At first, we are going to make sure that we have all the latest softwares updated on our ubuntu 24.04.2 LTS.<br>  
We simply run this code to do so. 
```bash
sudo apt update && sudo apt upgrade -y
```
# 2. Snap package manager installed or not?
Then, we check if snap package is instaled or not by: 
```bash
snap --version
```
If available, it will display the version, else it says command not found.<br>
If not installed, just install it using this command:
```terminal
sudo apt install snapd -y
```
# 3. Install next cloud

Installing next cloud is super simple thanks to snap which handles 10+ manual configurations all by itself. It configures databases, php and web servers automatically. Just running this command, next cloud will be installed!
```bash
sudo snap install nextcloud
```
 Check if installed or not:
```bash
 sudo nextcloud.occ --version
 ```
# 4. Check information of next cloud
Now, we have to check if next cloud is functioning properly or not. Run a simple command:
```
sudo snap services nextcloud
snap info nextcloud
```
Now once you know that next cloud is enabled/active, create your id with:<br>
(replace the variables)
```bash
sudo nextcloud.manual-install yourusername yourpassword
```
It will output as: 

### Nextcloud was successfully installed.

# 5. Check ports 
Next cloud could run in two ports: one for each of http and https. Check the ports by this command.

```bash
sudo snap get nextcloud ports
```
You will get key value pair for http and https ports.

# 6. Check ports availability

Sometimes, services like apache2 might be blocking port 80. Check if thats the case by:
```bash
sudo netstat -tlnp | grep :80
```
If you see something like this:
```output
tcp6       0      0 :::80                   :::*                    LISTEN      1379/apache2
```
Then you need to stop and disable apache2 or any other service that might override the port. Simply do:
```bash
sudo systemctl stop apache2
```
```bash
sudo systemctl disable apache2
```
Now you can restart nextcloud by:
```bash
sudo snap restart nextcloud
```
Now, we need to find ip address of our device. To do that simply:
```bash
 ip addr show | grep inet
```
 ###The ip with format 192.168.1.__ is mostly our ip.

 That ip should be added to trusted domains with:
```bash
 sudo nextcloud.occ config:system:set trusted_domains 1 --value=192.168.1.__
```
 # open firewall for phone access
Now, it is setup in your localhost. You can access the nextcloud server from you pc easily.<br>
To access it from phone, open firewall with this command:
```bash
 sudo ufw allow 80
```
# Work in phone

now install the app or browse the official next cloud website from your phone. Enter the ip address for the host i.e. 192.168.1.__ . Then enter your login credentials to gain access to the cloud!

 


