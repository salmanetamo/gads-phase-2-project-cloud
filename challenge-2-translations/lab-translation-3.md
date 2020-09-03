# LAB: Creating Virtual Machines
**Channel** :  *Associate Cloud Engineer - Learning Phase 1 Main Track Channel*
**Course**: *Essential Google Cloud Infrastructure: Core Services*
**Module**: *Storage annd Database Services*
**Lab**: *Implementing Cloud SQL*

## Objectives
In this lab, you learn how to perform the following tasks:

- Create a Cloud SQL database

- Configure a virtual machine to run a proxy

- Create a connection between an application and Cloud SQL

- Connect an application to Cloud SQL using Private IP address

## Steps and Translation
### Task 1: Create a Cloud SQL database
#### Creating a MySQL instance 
For a private Ip address, there is a need to create an allocated IP range for services as well as a Private connection inside our default network.

- Allocating an IP address range  
    `gcloud compute addresses create google-managed-services-default --global --purpose=VPC_PEERING     --prefix-length=16 --description="peering range for Google" --network=default`
- Creating a private connection to the newly created Reserved address range  
    `gcloud services vpc-peerings connect --service=servicenetworking.googleapis.com --ranges=google-managed-services-default --network=default --project=qwiklabs-gcp-02-ebf96b4b0614`
- Creating the Cloud SQL instance with the provided configuration  
    `gcloud beta sql instances create wordpress-db --root-password=password --region=us-central1 --database-version=MYSQL_5_7 --network=https://www.googleapis.com/compute/alpha/projects/qwiklabs-gcp-02-ebf96b4b0614/global/networks/default  --no-assign-ip  --tier=db-n1-standard-1`

---

### Task 2: Configure a proxy on a virtual machine
1. #### Connect via SSH to `wordpress-europe-proxy`  
    `gcloud compute ssh wordpress-europe-proxy --zone europe-west1-b`
2. #### Downloading the Cloud SQL Proxy and making it executable  
    `wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy && chmod +x cloud_sql_proxy`
3. #### Getting the Cloud SQL instance connection name  
    - `gcloud sql instances describe wordpress-db`  
        - **Output (connectionName property)**: *qwiklabs-gcp-02-ebf96b4b0614:us-central1:wordpress-db*
4. #### Creating a a database `wordpress`

    `gcloud sql databases create wordpress --instance=wordpress-db`

5. #### Saving connection name in environment variable and verifying  
    - `export SQL_CONNECTION=[SQL_CONNECTION_NAME]`
    - `echo $SQL_CONNECTION`
5. #### Activating the proxy connection to the Cloud SQL database and sending process to the background  
    `./cloud_sql_proxy -instances=$SQL_CONNECTION=tcp:3306 &`

---

### Task 3: Connect an application to the Cloud SQL instance
1. #### Finding the external IP of the virtual machine  
    `curl -H "Metadata-Flavor: Google" http://169.254.169.254/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip && echo`

1. #### Finding the external IP of wordpress-europe-proxy
    - `gcloud compute instances describe wordpress-europe-proxy`  
        - **Output (natIP Property)**: *35.233.23.119*
    
2. #### Configuring the Wordpress application in the browser
    *No Translation required* 

---

### Task 4: Connect to Cloud SQL via internal IP
1. #### Getting Private IP address of the Cloud SQL server
    - `gcloud sql instances describe wordpress-db`
        - **Output (ipAddress Property)**: *10.31.0.3*
2. #### Getting external IP of `wordpress-us-private-ip`
    - `gcloud compute instances describe wordpress-us-private-ip`
        - **Output (natIP Property)**: *34.68.2.137*
3. #### Configuring the Wordpress application in the browser  
    *No Translation required* 

---

### Task 5: Review
*No Translation required* 
