Here is your Ansible lab formatted as a `README.md`:

````markdown
# 🧪 Lab 1.1: Install Ansible, Create Inventory File, and Run Ad-Hoc Commands

This lab will guide you through installing Ansible, setting up an inventory file, and running basic ad-hoc commands between two Ubuntu 20.04 virtual machines.

---

## 🧾 Requirements

- Two Ubuntu 20.04 VMs  
  - **VM 1**: `192.168.1.13` - Control Node (`control-node.example.com`)
  - **VM 2**: `192.168.1.14` - Managed Node (`managed-node.example.com`)

---

## 🧰 Steps

### 1. Set Hostnames

#### On Control Node:
```bash
sudo hostnamectl set-hostname control-node.example.com
hostname
````

**Expected Output:**

```bash
control-node.example.com
```

#### On Managed Node:

```bash
sudo hostnamectl set-hostname managed-node.example.com
hostname
```

**Expected Output:**

```bash
managed-node.example.com
```

---

### 2. Update `/etc/hosts` File

#### On Both Nodes:

Edit `/etc/hosts` to include:

```bash
127.0.0.1 localhost
192.168.1.13 control-node.example.com control-node
192.168.1.14 managed-node.example.com managed-node
```

---

### 3. Setup Password-less SSH

#### On Control Node:

Generate SSH key:

```bash
ssh-keygen -t rsa
```

Copy the public key to the managed node:

```bash
ssh-copy-id ubuntu@192.168.1.14
```

Ensure permissions on managed node:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

### 4. Add User to Sudoers (If Needed)

On both nodes, make sure your user can run sudo:

```bash
sudo usermod -aG sudo $USER
```

---

### 5. Install Ansible (Control Node Only)

```bash
sudo apt-get update
sudo apt-get -y install ansible
```

---

### 6. Create Inventory File

#### On Control Node:

```bash
mkdir -p ~/playbooks
cd ~/playbooks
cat <<EOF > hosts.ini
[servers]
192.168.1.14
EOF
```

---

### 7. Run Ansible Ad-Hoc Commands

#### ✅ Ping Check:

```bash
ansible all -m ping -i hosts.ini
```

#### 📁 List Files in `/tmp`:

```bash
ansible servers -m command -a "ls /tmp" -i hosts.ini
```

#### 🔄 Update APT Cache:

```bash
ansible servers -i hosts.ini -m apt -a "update_cache=yes" --become
```

#### 🌐 Install Apache2:

```bash
ansible servers -m apt -a "name=apache2 state=present" -i hosts.ini --become
```

#### 🧪 Verify on Managed Node:

```bash
dpkg -l | grep apache2
```

---

## ✅ Lab Completed

You’ve successfully:

* Installed Ansible
* Set up an inventory file
* Verified host connectivity
* Executed ad-hoc Ansible commands

---

```

Let me know if you'd like this broken into multiple files or converted into a GitHub-ready project structure!
```
