# security-onion-install-tutorial
This is a tutorial on installing a Security Onion instance on VirtualBox, with an Ubuntu VM to access the analyst interface.

- Minimum hardware recommendation: 250GB, 16GB RAM, 6 cores of CPU.


### Content
[Downloading Security Onion ISO](https://github.com/borelli28/security-onion-install-tutorial#downloading-security-onion-iso)

[Settings of Security Onion VM in VirtualBox](https://github.com/borelli28/security-onion-install-tutorial#settings-of-security-onion-vm-in-virtualbox)

[Security Onion instance setup](https://github.com/borelli28/security-onion-install-tutorial#security-onion-instance-setup)

[Settings Ubuntu VM](https://github.com/borelli28/security-onion-install-tutorial#settings-ubuntu-vm)

[Adding analyst machine to Security Onion firewall so we can access the interface](https://github.com/borelli28/security-onion-install-tutorial#adding-analyst-machine-to-security-onion-firewall-so-we-can-access-the-interface)


#### Downloading Security Onion ISO
- Visit the repo and click on the download link: https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md

- Check the SHA256sum hash of the downloaded file. It should match with the one in the repo: `sha256sum securityonion-2.3.260-20230620.iso`
	output: `06ed74278587b09167fbac1e5796b666fc24ad15d06ea3cc36419d07967e06dd  securityonion-2.3.260-20230620.iso`


#### Settings of Security Onion VM in VirtualBox

- Now we launch VirtualBox and start creating the VM instance for Security Onion:
![alt text](./images/sec-install-0.png)
Make sure to select "Ubuntu(64-bit)" version and check [x]"Skip Unatttended Installation".

- For Hardware, we are selecting 12288MB(12GB) and 4 CPU's, which are the minimum requirements that Security Onion recommends. https://docs.securityonion.net/en/2.3/hardware.html#hardware

![alt text](./images/sec-install-1.png)

- For Hard Disk, we are selecting 200GB which is the minimum recommended.

![alt text](./images/sec-install-2.png)

- Now we are clicking on settings for the seconion VM. We are disabling audio, which we don't need. For Network, we will have two adapters; the first one will be a NAT Network for the interface & the second one will be a Bridged Adapter with Promiscuous Mode to "Allow VMs" for monitoring.

![alt text](./images/sec-install-3.png)

![alt text](./images/sec-install-4.png)
Please note the MAC address, so you can select the right Adapter during setup.

![alt text](./images/sec-install-5.png)
Promiscuous mode allows the adapter to collect all the traffic going through the network.


#### Security Onion instance setup

- Now we press "Start" while selecting the seconion VM to start the instance.

- Let the timer run out to start the automatic boot, and type yes in the next screen

![alt text](./images/sec-install-6.png)

- Enter an username: `admin`

- Enter password and re-type.

- Now a bunch of packages will be installed so just wait.

![alt text](./images/sec-install-7.png)

- When it's done we will press enter to reboot and continue the setup.

![alt text](./images/sec-install-8.png)

- Login, and press "Yes" to continue with the setup.

- Select Install

![alt text](./images/sec-install-9.png)

- Select EVAL

- Type "agree" and press "OK".

- You may get a screen which let's you know that your hardware for the instance is under the minimum recommended press "Yes" to continue(12Gb = 12,288MB not 12,000MB).

- Enter a hostname for the instance and press "OK".

![alt text](./images/sec-install-10.png)

- In this screen we select the Network Adapter for management, which would be the Internal Network adapter. Verify the MAC address to pick the correct one.

![alt text](./images/sec-install-11.png)

- Select "DHCP" and then press "OK".

- Press "Yes" to continue with a DHCP.

- Press "OK" to setup the networking.

![alt text](./images/sec-install-12.png)

- Select "Standard" for type of manager.

- Select "Direct".

- Select the network adapter for Monitoring.

![alt text](./images/sec-install-13.png)

- Select "Automatic" for OS path schedule.

- Press "OK" to select the default home network IP's.

- Press "OK" for enabling all services for the instance.	

![alt text](./images/sec-install-14.png)

- Press "Yes" to accept default docker IP range.

- Enter an email to access the interface later on and password.

- Select "IP".

- Press "Yes" to configure NTP servers.

- Press "Ok" to select the default.

- And press "No" for running so-allow right now, since we will be doing it later when we setup our Ubuntu VM.

![alt text](./images/sec-install-15.png)

- Take a screenshot of the screen since you are going to need the access URL for the interface later, and press "Yes".

- Now we will be waiting for a while until the security onion finish setting up the instance for us.

![alt text](./images/sec-install-16.png)

Once it is done we can shut down the instance and move up to setting up our Ubuntu VM.

![alt text](./images/sec-install-17.png)


#### Settings Ubuntu VM

- Go to the link and download the Ubuntu desktop LTS ISO: https://ubuntu.com/download/desktop 

- When is done downloading, verify the SHA256 hash of file. You can find the SHA256 hash in the download page of Ubuntu.

- Now we press "New" to start creating our Ubuntu VM:

![alt text](./images/ubuntu-0.png)

- Now for Hardware you can as many CPU cores as you want but at least 2, and 2GB of RAM(Base memory).

![alt text](./images/ubuntu-1.png)

- For Hard Disk, you can leave it at 25GB or more if you want, and press "Finish".

- For Network, switch adapter 1 to a NAT Network, and pick the network name that you used for the Security Onion instance to make sure they can communicate.

![alt text](./images/ubuntu-2.png)

- Now we select the ubuntu instance and press "Start".

- Select "Try or Install Ubuntu".

![alt text](./images/ubuntu-3.png)

- Select language and "Install Ubuntu".

- Select keyboard layout.

- Leave the default and press "Continue".

![alt text](./images/ubuntu-4.png)

- Select "Erase disk and Install Ubuntu" and press "Install Now".

- Press "Continue" and select you location.

- Now pick you username, name for the PC, and password. Press "Continue".

![alt text](./images/ubuntu-5.png)

- At the end of the installation we need to restart the VM and then press Enter.

![alt text](./images/ubuntu-6.png)

- Enter password to login.

![alt text](./images/ubuntu-7.png)

- Now open the app Terminal by clicking on Activities(Upper left corner), and type "terminal".

![alt text](./images/ubuntu-8.png)

- Run update in the terminal, when prompted enter your password: `sudo apt update`.

- Now run `ip addr` in order to get the private IPv4 of this instance so we can set it up on the Security Onion instance

![alt text](./images/ubuntu-9.png)

It should look like the IP above. Please note the IP, we are going to needed in the next step.

- Now we can leave the Ubuntu instance running while we start the security onion instance.


#### Adding analyst machine to Security Onion firewall so we can access the interface

- Login into the Security Onion VM.

- Note the Security Onion web interface URL, it should look something like this: `https://10.0.2.5`.

- Now we add the IP of our analyst instance to SO in one single command like this: `sudo so-allow -a -i 10.0.2.4`.
	- `sudo` super-user do.
	- `so-allow`: Wazuh safe list.
	- `-a`: analyst.
	- `-i`: IP.

![alt text](./images/ubuntu-10.png)

- Enter password and wait until is done. Then we can go to our Ubuntu analyst instance to check if we get access to the interface.

- In the Ubuntu analyst instance we open terminal and we first ping google.com to check for Internet connection.

- Then we ping the Security Onion instance to check for connection.

- If the packets were received, that means we should be able to get access to the interface.

![alt text](./images/ubuntu-11.png)

- Login with the email and password that you used when we were setting up Security Onion.

![alt text](./images/ubuntu-12.png)



