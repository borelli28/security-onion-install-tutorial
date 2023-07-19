# security-onion-install-tutorial
This is a tutorial on installing a Security Onion instance on a Virtualbox VM, with an Ubuntu VM to access the analyst interface.


### Downloading Security Onion ISO
- Visit the repo and click on the download link: https://github.com/Security-Onion-Solutions/securityonion/blob/master/VERIFY_ISO.md

- Check the SHA256sum hash of the downloaded file. It should match with the one in the repo: `sha256sum securityonion-2.3.260-20230620.iso`
	output: `06ed74278587b09167fbac1e5796b666fc24ad15d06ea3cc36419d07967e06dd  securityonion-2.3.260-20230620.iso`

- Now we launch VirtualBox and start creating the VM instance for Security Onion:
![alt text](./images/sec-install-0.png)
Make sure to select "Ubuntu(64-bit)" version and check "Skip Unatttended Installation".

- For Hardware, we are selecting 12288MB(12GB) and 4 CPU's, which are the minimum requirements that Security Onion recommends. https://docs.securityonion.net/en/2.3/hardware.html#hardware

![alt text](./images/sec-install-1.png)

- For Hard Disk, we are selection 200GB which is the minimum recommended.

![alt text](./images/sec-install-2.png)

- Now we are clicking on settings for the seconion VM. We are disabling audio, which we don't need. For Network, we will have two adapters; the first one will be a NAT Network for the interface & the second one will be a Bridged Adapter with Promiscuous Mode to "Allow VMs" for monitoring.

![alt text](./images/sec-install-3.png)
This step is optional.

![alt text](./images/sec-install-4.png)
Please note the MAC address so you can select the right Adapter during setup.

![alt text](./images/sec-install-5.png)
Promiscuous mode allows the adapter to collect all the traffic going through the network.

- Now we press "Start" while selecting the seconion VM to start the instance.

- Let the timer run out to start the automatic boot, and type yes in the next screen

![alt text](./images/sec-install-6.png)

- Enter an username: `admin`

- Enter password and re-type.

- Now a bunch of packages will be installed so just wait.

![alt text](./images/sec-install-7.png)

- When it's done we will press enter to reboot and continue the setup.

![alt text](./images/sec-install-8.png)

- Login, and pre "Yes" to continue with the setup.

- Select Install

![alt text](./images/sec-install-9.png)

- Select EVAL

- Type "agree" and press "OK".

- You may get a screen which let's you know that your hardware for the instance is under the minimum recommended press "Yes" to continue(12Gb = 12,288MB not 12,000MB).

- Enter a hostname for the instance and press "OK".

![alt text](./images/sec-install-10.png)

- In this screen we select the Network Adapter for management, which would be the Internal Network adapter. Verify MAC address to pick the correct one.

![alt text](./images/sec-install-11.png)

- Select "DHCP" and then press "OK".

- Press "Yes" to continue with a DHCP.

- Press "OK" to setup the networking.

![alt text](./images/sec-install-12.png)




