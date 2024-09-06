# Deploy Artifacts on a Container with Ansible

![image](https://github.com/user-attachments/assets/f01352fb-c87e-4ca2-8879-0d8e6c2bf7b6)

## Setup CI/CD with GitHub, Jenkins, Maven, Ansible & Docker.
- Integrate Docker Host with Ansible.
- Ansible playbook to create Image.
- Ansible playbook to create Container.
- Integrate Ansible with Jenkins.
- CI/CD Job to build code on Ansible & Deploy it on docker container.


## Jenkins Stages:
To set up a Jenkins pipeline that performs the following actions:
- **Checkout Code**: Automatically triggers when a change is pushed to GitHub.
- **Build with Maven**: Maven to compile the Java code, run unit tests, and package the application (usually into a .war file for a web application).
- **Build Docker Image**: This stage involves building a Docker image that contains your packaged application (e.g., .war file) and the necessary runtime environment. 
- **Push Docker Image**	:This stage pushes the newly built Docker image to a remote registry so that it can be pulled and used in various environments (e.g., production, staging).
- **Deploy to Tomcat Container (Docker)**:  Pipeline deploys the Docker container running Tomcat. It can either pull the latest Docker image and start the container or update the existing one.
- **Copy .war to Docker Container**: Deploys the resulting .war file to a Tomcat server.


## Prerequisites

### Server Installation
- **Jenkins** : Jenkins should be installed and accessible. **[Installation](https://github.com/manishktomar/bash-scripts)**
- **Maven** : Maven should be installed and accessible from Jenkins **[Installation](https://github.com/manishktomar/bash-scripts)**
- **Docker**: Docker should be installed and accessible from Jenkins **[Installation](https://github.com/manishktomar/bash-scripts)**
- **Ansible**: Ansible should be installed and accessible from Jenkins **[Installation](https://github.com/manishktomar/bash-scripts)**
- 
### Jenkins Plugin Installation and Setup
- **Credentials**: Credentials for GitHub and Dockerhub should be configured in Jenkins.

## Ansible Playbook to create image and container
**Step 1** Create Username and password for Ansible
    ```
    useradd ansadmin
    passwd ansadmin
    visudo                                    //Set Sudo permission
        ansadmin ALL=(ALL)  NOPASSWD: ALL
    ```

**Step 2** Configure ssh-key for ansible host
    ```
    ssh-keygen
    ssh-copy-id **IP**                       //Copy ssh-key on server for deoployment 
    ```

**Step 3** vi /etc/ansible/hosts            // Add Host on Ansible 
           **Add host IP**  

    Testing for Host:
    ```
    ansible all -m ping
    ansible $hostname -m ping
    ansible all -m command -a uptime
    ```

**Step 4** Create ansible playbook and deploy.
    ```
    ansible-playbook ansible.yml --check        // Ansible.yml is Playbook name.
    ansible-playbook ansible.yml
    ```

## Errors and Solutions: 

#### Issue 1 
