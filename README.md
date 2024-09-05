# Proxmox

Here's an extensive list of Proxmox Virtual Environment (PVE) CLI commands and configurations, categorized for ease of use.

### **Proxmox CLI Commands**

#### **1. System Information and Management**

- **View Proxmox version:**
  ```bash
  pveversion
  ```

- **Check system status:**
  ```bash
  pvecm status
  ```

- **View node information:**
  ```bash
  pvecm nodes
  ```

- **Show cluster status:**
  ```bash
  pvecm status
  ```

- **List all storage configuration:**
  ```bash
  pvesh get /storage
  ```

- **Show node status:**
  ```bash
  pveperf
  ```

- **List all configured network interfaces:**
  ```bash
  ip a
  ```

- **View logs for the Proxmox cluster:**
  ```bash
  journalctl -u pve-cluster
  ```

#### **2. VM and Container Management**

- **List all VMs and containers:**
  ```bash
  qm list
  pct list
  ```

- **Start a VM:**
  ```bash
  qm start VM_ID
  ```

- **Stop a VM:**
  ```bash
  qm stop VM_ID
  ```

- **Reboot a VM:**
  ```bash
  qm reboot VM_ID
  ```

- **Shutdown a VM:**
  ```bash
  qm shutdown VM_ID
  ```

- **Create a new VM:**
  ```bash
  qm create VM_ID --name VM_NAME --memory MEMORY_SIZE --net0 virtio,bridge=vmbr0 --scsihw virtio-scsi-single --disk size=DISK_SIZE,format=qcow2
  ```

- **Delete a VM:**
  ```bash
  qm delete VM_ID
  ```

- **View VM configuration:**
  ```bash
  qm config VM_ID
  ```

- **Modify VM configuration:**
  ```bash
  qm set VM_ID --memory NEW_MEMORY_SIZE --net0 NEW_NET_CONFIG
  ```

- **List container status:**
  ```bash
  pct status CONTAINER_ID
  ```

- **Start a container:**
  ```bash
  pct start CONTAINER_ID
  ```

- **Stop a container:**
  ```bash
  pct stop CONTAINER_ID
  ```

- **Create a new container:**
  ```bash
  pct create CONTAINER_ID TEMPLATE_ID --hostname CONTAINER_NAME --memory MEMORY_SIZE --net0 name=eth0,bridge=vmbr0,ip=IP_ADDRESS/24 --rootfs STORAGE:SIZE
  ```

- **Delete a container:**
  ```bash
  pct delete CONTAINER_ID
  ```

#### **3. Storage Management**

- **List storage configurations:**
  ```bash
  pvesh get /storage
  ```

- **Add a new storage configuration:**
  ```bash
  pvesh create /storage --storage STORAGE_NAME --type TYPE --content CONTENT_TYPE
  ```

- **Remove a storage configuration:**
  ```bash
  pvesh delete /storage/STORAGE_ID
  ```

- **List all storage volumes:**
  ```bash
  lsblk
  ```

- **Resize a storage volume:**
  ```bash
  lvresize -L SIZE VOLUME_PATH
  ```

- **Create a new volume group:**
  ```bash
  vgcreate VOLUME_GROUP_NAME /dev/device
  ```

- **Create a new logical volume:**
  ```bash
  lvcreate -L SIZE -n VOLUME_NAME VOLUME_GROUP_NAME
  ```

#### **4. Networking**

- **Show network configuration:**
  ```bash
  ip a
  ```

- **Edit network configuration:**
  ```bash
  nano /etc/network/interfaces
  ```

- **Restart networking service:**
  ```bash
  systemctl restart networking
  ```

- **Show bridge configuration:**
  ```bash
  brctl show
  ```

#### **5. Backup and Restore**

- **Create a backup of a VM:**
  ```bash
  vzdump VM_ID --storage STORAGE_ID --mode snapshot
  ```

- **Restore a VM from backup:**
  ```bash
  qmrestore BACKUP_FILE VM_ID --storage STORAGE_ID
  ```

- **List backups:**
  ```bash
  ls /var/lib/vz/dump/
  ```

- **Delete a backup:**
  ```bash
  rm BACKUP_FILE
  ```

#### **6. Cluster Management**

- **Join a new node to the cluster:**
  ```bash
  pvecm add CLUSTER_NODE_IP
  ```

- **Remove a node from the cluster:**
  ```bash
  pvecm delnode NODE_NAME
  ```

- **Check cluster quorum:**
  ```bash
  pvecm status
  ```

- **View cluster logs:**
  ```bash
  journalctl -u pve-cluster
  ```

#### **7. User and Permission Management**

- **List all users:**
  ```bash
  pveum user list
  ```

- **Create a new user:**
  ```bash
  pveum user add USERNAME@REALM --password PASSWORD
  ```

- **Delete a user:**
  ```bash
  pveum user delete USERNAME@REALM
  ```

- **List all roles:**
  ```bash
  pveum role list
  ```

- **Assign a role to a user:**
  ```bash
  pveum aclmod /path/to/target --user USERNAME@REALM --role ROLE
  ```

- **Remove a role from a user:**
  ```bash
  pveum aclrm /path/to/target --user USERNAME@REALM
  ```

#### **8. Advanced Configuration**

- **Edit Proxmox configuration files:**
  ```bash
  nano /etc/pve/pve.conf
  ```

- **View Proxmox logs:**
  ```bash
  tail -f /var/log/pve/tasks/*.log
  ```

- **Check and manage Proxmox services:**
  ```bash
  systemctl status pve-cluster
  systemctl restart pve-cluster
  ```

- **Update Proxmox packages:**
  ```bash
  apt-get update && apt-get upgrade
  ```

- **Synchronize time with NTP:**
  ```bash
  systemctl restart systemd-timesyncd
  ```

- **Set up a new Proxmox storage type (e.g., Ceph):**
  ```bash
  pveceph install
  ```

#### **9. Monitoring and Troubleshooting**

- **Monitor Proxmox node performance:**
  ```bash
  pveperf
  ```

- **Check disk space usage:**
  ```bash
  df -h
  ```

- **Monitor system resources:**
  ```bash
  top
  ```

- **Check for hardware errors:**
  ```bash
  dmesg | grep -i error
  ```

- **Verify disk and file system health:**
  ```bash
  smartctl -a /dev/sdX
  ```

### **Summary**

This extensive guide provides a comprehensive set of `proxmox` commands and configurations for managing Proxmox VE, covering a wide range of tasks including system management, VM and container management, storage management, networking, backups, clustering, user permissions, advanced configurations, and troubleshooting.
