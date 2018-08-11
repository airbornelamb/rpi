# Raspberry Pi 3

This is my repo for testing configurations on my rpi3. So far what this repo will do is use cloud-init on top of Hypriot to setup a Docker swarm with Portainer and Pi-Hole. You'll have a swarm and ad-blocking DNS in less than the time it takes to brew a cup of coffee.

## Usage

**I would suggest forking this repo so you can make changes to any config files. Or you could use mine, but the key is to remember I have set the address to 192.168.2.2 for the pi in multiple config files and you will have to either go with that or change it.**

First you will need to get the amazing Hypriot flash utility:
```bash
curl -LO https://github.com/hypriot/flash/releases/download/2.1.1/flash
chmod +x flash
sudo mv flash /usr/local/bin/flash
```

You can then download and edit the user-data.yml of this repo:
`wget https://raw.githubusercontent.com/airbornelamb/rpi/master/user-data.yml`

You'll particularly want to change the username, ssh authorized keys (from cat ~/.ssh/id_rsa.pub) and timezone.

After that you are ready to flash the SD card
```bash
flash \
  --hostname pi.local \
  --userdata ./user-data.yml \
  https://github.com/hypriot/image-builder-rpi/releases/download/v1.9.0/hypriotos-rpi-v1.9.0.img.zip
```

If all goes well, the pi will boot up and run cloud-init using user-data.yml. It will automatically resize the root partition, create the user, update and install debian packages, clone this repo, initialize a docker swarm, start a portainer stack, and start a pi-hole stack (using pihole-stack.yml) with volumes mounted in the cloned repo at /var/rpi/pihole

You now have two web admin interfaces:

http://192.168.2.2:9000 is running Portainer. You can browse here and create the first admin user.

http://192.168.2.2/admin is running pi-hole. The DNS forwards to cleanbrowsing.org by default and there is no admin password set.


Sources:

https://github.com/hypriot/image-builder-rpi

http://cloudinit.readthedocs.io/en

https://github.com/pi-hole/docker-pi-hole

https://github.com/pi-hole/docker-pi-hole/blob/master/doco-example.yml

https://hub.docker.com/r/pihole/pihole/

https://hub.docker.com/r/pihole/pihole/tags/

https://docs.docker.com/v17.12/edge/engine/reference/commandline/service_create

https://stackoverflow.com/questions/49950326/how-to-create-docker-volume-with-files-or-cp-files-into-it

https://superuser.com/questions/827977/use-cloud-init-with-virtualbox

Alternatives:

https://github.com/davidferguson/pibakery

https://github.com/FooDeas/raspberrypi-ua-netinst
