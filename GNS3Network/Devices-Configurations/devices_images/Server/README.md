# Ubuntu Cloud Image

Ubuntu Cloud Guest using NoCloud in 12.04 and later. The cloud-utils package included in 12.10 and later contains a tool cloud-localds that helps in creating this data.


```
## Install a necessary packages
$ sudo apt install cloud-image-utils

## URL to most recent cloud image of 22.04
$ img_url="https://cloud-images.ubuntu.com/jammy/current/jammy-server-cloudimg-amd64.img"
## download the image
$ wget $img_url -O disk.img

## Create a file with some user-data in it
$ cat > userdata <<EOF
password: ubuntu
chpasswd: { expire: False }
ssh_pwauth: True
EOF

## Convert the compressed qcow file downloaded to a uncompressed qcow2
$ qemu-img convert -O qcow2 disk.img disk.qcow2

## create the disk with NoCloud data on it.
$ cloud-localds userdata.img userdata

## Boot a kvm, this requires gtk by default
$ kvm -net nic -net user -hda disk.qcow2 -hdb userdata.img -m 1024

## when booting the kvm, you can use username "ubuntu" and password "ubuntu", after that, close the kvm, and disk.qcow2 is ready to be used
```