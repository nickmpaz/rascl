1. prepare raspbian image on SD card. touch ssh. wpa_supplicant.conf. for each raspi


2. check that each pi is on your local net with nmap. add ip's to inventory file (pis). 
4. get all mac addresses. fill in vars.yml with mac address mappings

3. run config playbook
$ ansible-playbook -k -i inventory setup.yml
---at this point--- 
all pis have new hostname, passwordless ssh, basic packages, and a static ip. MAYBE CHANGE PASSWORDS?    


5. check to make sure passwordless ssh works with
$ ansible -i inventory -m ping

6. run setup playbook to create cluster
$ ansible-playbook -i inventory setup.yml






# Rascl

Turn your Raspberry Pis into a k8s cluster with ansible and kubeadm

## Requirements

- Raspberry Pi(s)
- Local network
- Ansible

## Install Raspbian

For each Raspberry Pi:

l. Download Raspbian Lite

l. Write the image to an SD card

l. In the boot directory create 2 files:

    l. ssh

    l. wpa_supplicant.conf

    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=US

    network={
        ssid="Your network name/SSID"
        psk="Your WPA/WPA2 security key"
        key_mgmt=WPA-PSK
    }

l. boot devices and check they appear on the network

## Find the IP and MAC addresses of your Pis

update inventory file and variables

## Run the setup playbook

    $ ansible-playbook -k -i inventory setup.yml


-new hostname
-new password
-install basic packages
-static ip assignment
-passwordless ssh
-restart pi

## Run the kubernetes playbook

    $ ansible-playbook -i inventory rascl.yml

-disable swap
-install docker
-install kubeadm
-reboot
-wait for connection

## initialize master node

## join other nodes