# LAB: Creating Virtual Machines
**Channel** :  *Associate Cloud Engineer - Learning Phase 1 Main Track Channel*
**Course**: *Essential Google Cloud Infrastructure: Foundation*
**Module**: *Virtual Machines*
**Lab**: *Creating Virtual Machines*

## Objectives
In this lab, you explore the available options for VMs and see the differences between locations.

In this lab, you learn how to perform the following tasks:

- Create several standard VMs

- Create advanced VMs

## Steps and Translation
### Task 1: Create a utility virtual machine
1. #### Create a VM
    `gcloud compute instances create my-vm --zone=us-central1-c --machine-type=n1-standard-1 --subnet=default --no-address --image=debian-9-stretch-v20200805 --image-project=debian-cloud`

2. #### Explore the VM details
    `gcloud compute instances describe my-vm --zone us-central1-c`

3. #### Explore the VM logs
    *No Translation required*

---

### Task 2: Create a Windows virtual machine
1. #### Create a VM
    - `gcloud compute instances create my-windows-vm --zone=europe-west2-a --machine-type=n1-standard-2 --subnet=default --tags=http-server,https-server --image=windows-server-2016-dc-core-v20200813 --image-project=windows-cloud --boot-disk-size=100GB`  

    - `gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server`

    - `gcloud compute firewall-rules create default-allow-https --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server`

2. #### Set the password for the VM
    *No Translation required*

---

### Task 3: Create a custom virtual machine
1. #### Create a VM
    `gcloud compute instances create my-custom-vm --zone=us-west1-b --machine-type=custom-6-32768 --subnet=default --image=debian-9-stretch-v20200805 --image-project=debian-cloud --boot-disk-size=10GB`
2. #### Connect via SSH to your custom VM

    1. Connecting through SSH
        `gcloud compute ssh my-custom-vm --zone us-west1-b`
    2. Seeing information about unused and used memory and swap space on custom VM:
        `free`
    3. Seeing details about the RAM installed on VM:
        `sudo dmidecode -t 17`
    4. Verifying the number of processors:
        `nproc`
    5. Seeing details about the CPUs installed on VM:
        `lscpu`
    6. Stopping SSH connection:
        `exit`

---

### Task 4: Review
*No Translation required*
