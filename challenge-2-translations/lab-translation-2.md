# LAB: Creating Virtual Machines
**Channel** :  *Associate Cloud Engineer - Learning Phase 1 Main Track Channel*
**Course**: *Essential Google Cloud Infrastructure: Core Services*
**Module**: *Resource Monitoring*
**Lab**: *Error Reporting and Debugging*

## Objectives
In this lab, you learn how to perform the following tasks:

- Launch a simple Google App Engine application

- Introduce an error into the application

- Explore Cloud Error Reporting

- Use Cloud Debugger to identify the error in the code

- Fix the bug and monitor in Cloud Operations

## Steps and Translation
### Task 1: Create an application
1. #### Get and test the application
    1. Creating a local folder and getting the App Engine Hello world application
        - `mkdir appengine-hello`
        - `cd appengine-hello`
        - `gsutil cp gs://cloud-training/archinfra/gae-hello/* .`
    2. Running the application using the local development server in Cloud Shell
        `dev_appserver.py $(pwd)`
    3. Previewing application and stopping it
        *No Translation required*

2. #### Deploy the application to App Engine
    1. Deploying the application to App Engine
        `gcloud app deploy app.yaml`
    2. Previewing the application
        `gcloud app browse`
3. #### Introduce an error to break the application
    1. Examining the main.py file
        `cat main.py`
    2. Using the sed stream editor to change the import library to the nonexistent `webapp22`
        `sed -i -e 's/webapp2/webapp22/' main.py`
4. #### Re-deploy the application to App Engine
    1. Re-deploying the application to App Engine
        `gcloud app deploy app.yaml --quiet`
    2. Previewing the application
        `gcloud app browse`


---

### Task 2: Explore Cloud Error Reporting
*No Translation required*

### Task 3: Review
*No Translation required*