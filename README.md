# Born2beRoot

This project's goal is to help you set up your `Virtual Machine` under specific instructions to get you close and close to know more about to world of virtualization.


## Resources :
#### 📘 Articles
 - [Born2beRoot (Full guide)](https://mathieu-soysal.gitbook.io/born2beroot)
 - [Gitbook Guide](https://42-cursus.gitbook.io/guide/rank-01/born2beroot)
 - [Born2beRoot Ultimate Guide](https://github.com/DevAwizard/Born2BeRoot_Guide_by_anwu-yan)
 - [How to setup your VM ?](https://github.com/Thuggonaut/42IC_Ring01_Born2beRoot/)
 - [What is ?](https://github.com/amaitou/Born2beRoot)
 - [How to enable SSH](https://phoenixnap.com/kb/how-to-enable-ssh-on-ubuntu)
 - [How to setup UFW Firewall](https://phoenixnap.com/kb/configure-firewall-with-ufw-on-ubuntu#ftoc-heading-6)
 - [How to Add a User to a Linux Group](https://phoenixnap.com/kb/add-user-to-linux-group)
 - [How To Set Password Policies In Linux](https://ostechnix.com/how-to-set-password-policies-in-linux/)
 - [Useful Sudoers Configuring sudo Command in Linux](https://www.geeksforgeeks.org/useful-sudoers-configurations-for-setting-sudo-in-linux/)
 - [TTY Command in Linux](https://www.geeksforgeeks.org/tty-command-in-linux-with-examples/)

#### 💻 Videos
- [Linux Directories Explained in 100 Seconds](https://www.youtube.com/watch?v=42iQKuQodW4)
- [Linux File System](https://www.youtube.com/watch?v=A3G-3hp88mo)
- [Virtualization (Part 1): Hypervisors & VMs](https://www.youtube.com/watch?v=a75fC8xnBn8)
- [Virtualization (Part 2): How hypervisors work](https://www.youtube.com/watch?v=L0IDOQneyRE)
- [Virtualization in Arabic](https://www.youtube.com/watch?v=3HChgNmRYJU)
- [Introduction to LVM | Linux Academy](https://www.youtube.com/watch?v=dMHFArkANP8&list=PLAoA-usw1t-4sIlwNXKS2RIn0ZBx4VQhn)
- [Born2beRoot : Installation and partitioning](https://www.youtube.com/watch?v=73r3JbkCVy0)

## ⚠️ Need to know :

#### 🔷 How does a virtual machine work ? And what its purpose ?
    
- **Virtualization** is the process of creating virtual versions of physical resources, such as servers, storage, networks, or applications. **The purpose of virtualization** is to optimize resource utilization, improve efficiency, and reduce costs by allowing multiple virtual systems or applications to run on a single physical hardware.
---
#### 🔷 Hypervisor ?

- **Hypervisor** is a software that can manage and create a virtual machine on your host and there is two types of hypervisor:
- **Type1 (bare metal)** : which is installed directly on top of your host
- **Type2** : which is installed on top of your operating system
---
#### 🔷 What's the difference between Debian and Rocky? and If you choose one on another explain why?
-
---
#### 🔷 What's a partition ? And more generally how does LVM (Logical Volume Management) work ?
- **Partition** is a logically divided section of a physical storage device 

* **LVM (Logical Volume Manager)** is a software-based system in Linux for **managing disk storage dynamically**. **LVM** is built into Linux.

    - **Physical Volumes (PVs):**
        > These are raw storage devices (e.g., /dev/sda1).
        > LVM uses them as building blocks.

    - **Volume Groups (VGs):**
        > A pool of storage created by combining one or more physical volumes. 
        > 
        > Example: Combine a 500GB and a 1TB disk into a single 1.5TB volume group.

    - **Logical Volumes (LVs):**
        > Flexible, virtual partitions carved out of a Volume Group.
        >
        > Example: Create an LV for /, another for /home, and one for swap.
        > Logical volumes can be resized, moved, or combined dynamically.

- With **LVM**, adding a new disk is easy, and the storage is managed as a unified pool. Logical Volumes can grow without needing to repartition or move data manually. Applications and users don’t notice any changes.

- With **Manual partitioning**, each new disk requires extra effort to partition, format, and mount. It often leads to fragmented storage, with data scattered across multiple locations, making management more complex as the system grows.
---
#### 🔷 What's sudo ?
-
---
#### 🔷 What's SSH (Secure Shell) and what's the value of using it ?
-
---
#### 🔷 What's an UFW (Uncomplicated Firewall) and what's the value of using it ?
-
---
#### 🔷 What's the advantages/disadvantages of a strong password policy ? What can you say about its implementation ?
-
---
#### 🔷 What's APPArmor ?
-
---
#### 🔷 What's Cron ?
-
---
## 📋 Instructions :

#### 1. Create Virtual Machine with VirtualBox
> **Your hostname must be your “login” + 42 (ex: imellali42).**
>
> **You must create at least 2 encrypted partitions using LVM :**

```sh
0. boot
1. root (mandatory part)
2. swap (mandatory part)
3. home (mandatory part)
4. var (bonus part)
5. srv (bonus part)
6. tmp (bonus part)
7. var/log (bonus part)
```
> **You must install GRUB Boot loader in your disk !**
---
#### 2. Installing sudo using apt

```sh
imellali@imellali42:~$ su
root@imellali42:/home/imellali# apt install sudo
root@imellali42:/home/imellali# apt install vim
```

> **If sudo not working :**

```sh
root@imellali42:/home/imellali# vi /etc/sudoers
```
> **Then and add this to sudoers file :**

```sh
"your user" ALL=(ALL) ALL
```

> **Example :**
```sh
imellali ALL=(ALL) ALL
```
> **Save and quit vim, Then quit su and try sudo again.**

---
#### 3. Installing & Configuring SSH
    
> **To install ssh  :**

```sh
sudo apt install openssh-server
sudo systemctl status ssh (to check if ssh is active)
```
> **To edit port to 4242  :**

```sh
sudo vi /etc/ssh/sshd_config
port 4242 (edit this)
```
> **To make the connection not as a root :**

```sh
sudo vi /etc/ssh/sshd_config
PermitRootLogin no (edit this)
```
---   
#### 4. Installing & Configuring UFW
    
> **To install UFW :**

```sh
sudo apt install ufw
sudo ufw version (to check if UFW installed)
sudo ufw enable (to unable UFW)
```

> **To allow SSH connection :**

```sh
sudo ufw allow ssh
```

> **To configure UFW with port 4242 :**

```sh
sudo ufw status numbered
sudo ufw delete 1 (to remove port 22)
sudo ufw delete 2 (to remove port 22/v6)
sudo ufw allow 4242
sudo ufw status (check if only port 4242 is there)
```
---   
#### 5. Create a new user and assign it to a group
> **To create a new user :**

```sh
sudo adduser "username"
```
> **To create a new group :**

```sh
sudo addgroup "groupname"
```
> **To create a user to a group :**

```sh
sudo adduser "username" "groupname"
```
> **To check if the user is within a group:**

```sh
getent group
```
> **To delete a group or a user :**

```sh
sudo -r deluser "username" (-r to delete its directory in /home)
sudo delgroup "groupname"
```
---
#### 6. Set up a strong password policy
> **Step 1 : (Install this package to enforce password quality)**
 
```sh
sudo apt install libpam-pwquality
```

> **Step 2 :**

```sh
sudo vi /etc/login.defs
PASS_MAX_DAYS 30 It's the max days till password expiration
PASS_MIN_DAYS 2 It's the min days till password change
MAX_WARN_AGE 7 It's the days till password warning
```
> **Step 3 :**

```sh
sudo vi /etc/pam.d/common-password
minlen=10 -> The minimun characters a password must contain.
ucredit=-1 -> The password at least have to contain a capital letter.
lcredit=-1 -> The password at least have to contain a lowercase letter.
dcredit=-1 -> The passworld at least have to containt a digit.
maxrepeat=3 -> The password can not have the same character repeated three contiusly times.
reject_username -> The password can not contain the username inside itself.
enforce_for_root -> We will implement this password policy to root.

This rule will be on seperate line (not gonna be applied on root user) :
difok=7 -> The new password must have at least 7 different characters from the old password
```

---
#### 7. Create a simple script called [monitoring.sh](http://monitoring.sh/)
---

## Questions Aside :


- ➜ **What is the difference between creating new a partiition with type primary or logical ?**
    - Use **primary partitions** for boot-related purposes and operating systems.
    - Use **logical partitions** for additional storage or non-boot-critical partitions to save primary slots.

- ➜ **What is the meaning of jornaling file system (ext4, ext3) ?**

    - A file system is a method used by an operating system to store, retrieve, and organize data on a partition. Without a file system, a partition is just raw, unstructured storage.
    - When creating a partition, the system asks you to choose a **file system** (e.g., ext4, ext3, FAT32, swap, etc.). This decision determines how data will be stored, organized, and accessed on that partition. Each file system is optimized for different purposes

- ➜ **What is the meaning of mount point ?**

    - **Mount Point**: Determines where the partition’s contents appear in the file system.
    - Assigning appropriate mount points improves organization, security, and recoverability.
    - Ensures partitions are used for their intended purpose.

- ➜ **GRUB Boot loader ?**

    - GRUB is a **boot loader** that loads the operating system kernel into memory and transfers control to it.
    - Without a boot loader, your computer wouldn’t know how to start your operating system.

- ➜ **How to change the hostname**

    - To modify your hostname just use this command on your machine's terminal:
```sh
sudo hostnamectl set-hostname "new hostname"
```
