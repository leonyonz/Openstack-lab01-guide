# Openstack-lab01-guide
Guide for OpenStack lab NolSatu.id
 OPENSTACK LAB GUIDE ALA ALA @YONZLEON_AW 

1. Buat internal network pada openstack
Project > Network > Networks
Click Create Network
Network Name: net-int0
Admin State: UP
Create Subnet: Checked
Subnet Name: subnet-int0
Network Address: 10.1.x.0/24
IP Version: IPv4
Gateway IP: 10.1.x.1
Disable Gateway: Unchecked
Enable DHCP: Checked
Allocation Pools: 10.1.x.100,10.1.x.200
DNS Name Servers: 8.8.8.8


2. Buat router
Project > Network > Routers
Click Create Router
Router Name: router0
Admin State: UP
External Network: net-ext

Click router0
Click Interfaces
Click Add Interface
Subnet: subnet-int0

3. Buat ip static menggunakan network port
pada menu network > klik net-int0 >  port > create port
name > node0 > specify > fixed IP > masukan ip sesuai guide 10.1.x.y 
name > node1 > specify > fixed IP > masukan ip sesuai guide 10.1.x.y

4. Generate public key dan private key
#PASTIKAN POSISI TERMINAL PADA SSH GATEWAY
ssh-keygen > enter > passhprase kosong > enter
ll .ssh/
#########################################################################
# saat generate key  menggunakan `ssh-keygen'                           #
# psti akan muncul 2 key:                                               #
# id_rsa=private key                                                    #
# id_rsa.pub public key                                                 #
#                                                                       #
# public key: ditaruh di server yg akan di remote                       #
# priv key. untuk meremote server yg sudah di taruh pubkey              #
#########################################################################

5. Import Keypair
#salin public key dan import ke keypair openstack
cat .ssh/id_rsa.pub > salin
buka openstack > compute > keypair > import pubkey > name: key0 > paste > save

6. Tambahkan rule pada security group
Project > Network > Security Groups > Manage Rules

Click Add Rule
Rule: ALL ICMP
Direction: Ingress
Remote: CIDR
CIDR: 0.0.0.0/0

Click Add Rule
Rule: SSH
Remote: CIDR
CIDR: 0.0.0.0/0

7. deploy instance 
Project > compute > instance
Launch Instance 
name: podx-node0
source: ubuntu
flavor: 2vcpu 4gb 20gb HDD
Network: detach net-int0
Network Port: attach port node0
security group: default
Keypair: key0

DEPLOYY

8. Add floating IP di tiap node0
instance > menu dropdown > associate floating ip > + > submit

9. verifikasi instance melalui ssh-gateway
ping float_ip_instance

10. remote instance via ssh melalui ssh-gateway
ssh ubuntu@float_ip_instance

SUKSES. MAKASIH 
