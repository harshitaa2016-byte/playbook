# VMware Automation with Ansible

This project runs VMware PowerShell scripts on Windows hosts using Ansible. It runs scripts one by one and stops if any script fails.

---

## What it does

Runs these scripts in order on a Windows machine:

1. `Idrac_check.ps1` — Manage iDRAC power and reboot  
2. `ESXi-SSH-Manager.ps1` — Enable SSH and exit maintenance mode on ESXi hosts  
3. `Datastore-name-fixer.ps1` — Rename datastores  
4. `vcenters_cleanup.ps1` — Cleanup VMs/templates and enable SSH  
5. `vmware-site-checker.ps1` — Validate VMs and hosts across vCenters  

---

## Requirements

- Ansible installed on your Linux or Mac control machine  
- Windows host with:  
  - WinRM enabled and reachable  
  - PowerShell 5+  
  - VMware PowerCLI installed  
- Network access to VMware and iDRAC  

---

## Setup

1. Put your PowerShell scripts in the `files/` folder.  
2. Edit `inventory.ini` with your Windows host details:

    ```ini
    [windows]
    winhost ansible_host=192.0.0.0 ansible_user=Administrator ansible_password=YourPassword ansible_connection=winrm ansible_winrm_transport=basic
    ```

---

## Run the playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
The playbook copies scripts to C:\Temp and runs them in order.

Notes
The playbook stops if any script fails.

Make sure PowerCLI and dependencies are installed on Windows.

Use Ansible Vault for passwords if possible.
