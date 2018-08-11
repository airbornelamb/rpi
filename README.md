# rpi

## Flash hypriot to sd card using user-data.yml

So far:
- clout-init
- portainer on port 9000
- pihole

```bash
flash \
  --hostname pi.local \
  --userdata ./user-data.yml \
  https://github.com/hypriot/image-builder-rpi/releases/download/v1.9.0/hypriotos-rpi-v1.9.0.img.zip
```

Sources:

https://github.com/hypriot/image-builder-rpi
http://cloudinit.readthedocs.io/en
https://github.com/pi-hole/docker-pi-hole
https://github.com/pi-hole/docker-pi-hole/blob/master/doco-example.yml
https://hub.docker.com/r/pihole/pihole/
https://hub.docker.com/r/pihole/pihole/tags/
https://docs.docker.com/v17.12/edge/engine/reference/commandline/service_create

https://superuser.com/questions/827977/use-cloud-init-with-virtualbox

Alternatives:

https://github.com/davidferguson/pibakery
https://github.com/FooDeas/raspberrypi-ua-netinst
