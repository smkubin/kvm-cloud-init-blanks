######
# 1. Customize network and user data
# 2. Pack them to iso -> label cidata
#    (-R - long name support)
genisoimage -o cidata.iso -volid cidata -R meta-data network-config user-data vendor-data
# 3. Cleate overlay from a bas image file so it can be reused
qemu-img -f qcow2 -F qcow2 -b <base img> vm_disk.qcow2
# 4. Run VM
virt-install --name new_vm --memory 2048 --vcpus 2 --cdrom cidata.iso --disk path=vm_dosk.qcow2,format=qcow2 --os-variant centos-stream9 --graphics vnc --import 
