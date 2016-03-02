This repo gets you going with RancherOS on OpenStack.

[Packer](http://packer.io) is used with the qemu builder to create the image which can be imported to glance. It's expected all of these requirements are in place beforehand.

## Build
```
wget https://releases.rancher.com/os/latest/rancheros.iso
packer build packer-rancher.json
```

## Import
Packer will create a qcow2 type image in `output_rancher` dir. You can import it into glance:

```
  glance image-create --name RancherOS \
  --container-format bare \
  --disk-format qcow2 \
  --file output_rancher/rancheros
```

## Upgrade ISO checksum

If a new version is released, you have to update the `iso_checksum`. ```md5sum rancheros.iso``` is your friend

```
make md5-iso
```
# rancheros-openstack