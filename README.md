# CHANGING VM NAMES IN PROXMOX
## Did you forget to name that VM? I got you!

I cannot tell you how many times I’ve been chugging along building out a lab just to look back and realize I left a few of my VMs unnamed, which can add unnecessary confusion to a lab over time. So instead of slapping your forehead and destroying and building out a new VM like a maniac let's walk through how to retroactively add a name to our VMs the easy way!

So to change VM names in PROXMOX we will need to modify the name field within a VMs configuration file which can be located at: `/etc/pve/qemu-server/` within this folder you will find configuration files formatted as such <VMID>.conf. where VMID is the, usually, 3 digit VM number.

Let's take this Step by Step.

---

Tools Used:
- PROXMOX Node Shell
- Command line Text editor of your choice (e.g., nano, vim)

---
<img width="797" height="372" alt="Screenshot 2025-10-17 082407" src="https://github.com/user-attachments/assets/620965df-3419-4f37-b9d9-5575ab4f6f67" />


1. At the main Screen for PROXMOX, select your node under the datacenter line item on the left

2. Select the >_ Shell option on the submenu just to the right of the left server view menu
   
3. Here we will issue commands to get to the folder housing our VM configuration files.
`cd /etc/pve/qemu-server/`
here we can check on the configuration files for our VMs with:
`ls -la`

4. After we locate our desired VM configuration file lets pop that open and take a look at what's under the hood. ill be vim for file editing
`vim YourVmName.conf`
here is where you will see the configuration file settings, in our case the "name:" line item didn't exist so we can easily just add that item and place our desired name for the machine in question.

<img width="1061" height="530" alt="Screenshot 2025-10-17 083230" src="https://github.com/user-attachments/assets/0c790c58-e7ed-4b64-a705-8dc43760c48a" />

5. In vim we use the "i" button to enter insert mode and type in our "name:" line and name here i am titling our machine "PfSenseFW"

6. After we are done we can type `:wq` to write our changes to the configuration file and exit the file. we give it a few seconds and we should see the change in the VM name on the left hand server view menu area!

<img width="485" height="304" alt="Screenshot 2025-10-17 085344" src="https://github.com/user-attachments/assets/70730b27-3642-4884-b8a2-fec1a42cebd9" />


You may need to reboot the machine if its running, to do that you can use `qm restart <VMID>` to reboot that specific machine.
