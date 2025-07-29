## Overview
This repository contains a containerized e-commerce web application, comprising a Node.js backend API, a Single Page Application (SPA) frontend served by Nginx, and a MongoDB database for data storage.
All components are orchestrated using Docker Compose with multi-stage Dockerfiles for optimized image sizes.

## Content
-[Requirement](#Requirement/)
-[Running The Application](#Running-The-Application/)
-[Launching The Application](#Launching-The-Application/)
-[Uploading the Changes to Github](#Uploading-the-changes-to-Github/)
-[Image Versioning](#Image-Versioning/)

## Requirements.
Before you begin, ensure you have the following installed on your system:

Git: For cloning the repository.

Docker Engine & Docker Compose (for Linux): This is essential for building and running Docker containers. Ensure Docker is running before proceeding.
<img width="1048" height="334" alt="Screenshot from 2025-07-10 16-43-32" src="https://github.com/user-attachments/assets/3d31341b-3d7e-4053-b64f-f1f95dac7c20" />

<img width="1206" height="158" alt="Screenshot from 2025-07-10 16-45-29" src="https://github.com/user-attachments/assets/6106be67-c935-44ff-8b5e-5a56804672a2" />


## Getting Started: Running the Application.
Follow these steps to get the entire e-commerce platform up and running locally:

Clone the Repository: Open your terminal or command prompt and clone this repository to your local machine: Screenshot from 2025-07-10 16-43-32 Screenshot from 2025-07-10 16-45-29

## Launching the Application.
i) Build Images with Docker Compose: 
Navigate to the root directory of the cloned repository (where docker-compose.yml is located). Then, execute the following command: 
<img width="885" height="31" alt="Screenshot from 2025-07-10 16-17-02" src="https://github.com/user-attachments/assets/16761c20-7792-4edc-8311-38e3d72b4c07" />

The Docker compose build command is used to build or rebuild images for services defined in a docker-compose.yaml file

ii)Run the Containers Using (docker compose up) command to build, create start, and attach the containers for all services defined in the docker-compose.yaml file.
<img width="897" height="31" alt="Screenshot from 2025-07-10 16-25-57" src="https://github.com/user-attachments/assets/21fd409e-5085-44db-b409-6033b9b4dc54" />

iii) Stopping Containers 
Use (docker compose down) command to stop containers and to remove containers, networks, volumes and images created by the (up) command. Screenshot from 2025-07-10 16-34-26
<img width="897" height="31" alt="Screenshot from 2025-07-10 16-34-26" src="https://github.com/user-attachments/assets/b210606c-5a7b-44dc-a3e4-500c0c1bbe83" />


## Uploading the Changes to Github.
i). git status command 
This command will display the state of the working directory, showing the adjusted areas within the directory. Screenshot from 2025-07-10 16-45-29
<img width="894" height="256" alt="Screenshot from 2025-07-10 16-52-41" src="https://github.com/user-attachments/assets/3eb9739d-ad22-446e-af18-d28478900407" />

ii). git add command 
This command updates the index using the current content and making it ready for the next commit. Screenshot from 2025-07-10 17-34-32
<img width="967" height="252" alt="Screenshot from 2025-07-10 17-34-32" src="https://github.com/user-attachments/assets/ae2fc346-e548-4e44-9231-0871998d0ae0" />

iii). git commit command 
The command adds and commit files to the git repository. Screenshot from 2025-07-10 17-42-03
<img width="1240" height="117" alt="Screenshot from 2025-07-10 17-42-03" src="https://github.com/user-attachments/assets/1cf5fedd-7bf0-4b08-ae89-c4432c56ef9c" />

iv). git push command 
This command is used to upload local repository content to a remote repository
<img width="803" height="175" alt="Screenshot from 2025-07-10 18-04-35" src="https://github.com/user-attachments/assets/dc7d698c-8d0b-4168-8135-201c5687370a" />

## Image Versioning.
Images can be versioned as per the changes made on it then pushed to docker hub repository for access. In this case, the dockerhub images have already defined by;
image: kenanricky/ricky-ecommerce-backend:v1.0.0
image: kenanricky/ricky-ecommerce-frontend:v1.0.0

After the images created, they can be pushed to dockerhub using the command "docker push"
<img width="1494" height="430" alt="Screenshot from 2025-07-10 20-47-33" src="https://github.com/user-attachments/assets/38cb336b-06dd-4547-9dd8-66abb749010e" />

# Ansible & Vagrant Provision
## Prerequisites
Install the following tools:
VirtualBox
Vagrant
Ansible
Docker Hub account (for image hosting)

After installation, verify that the installation is successful.


# Procedures

First, access the repository where you'll be working from.

# Clone the repository
cd yolo-ecommerce-deployment to the working repository.<br/>
"git clone https://github.com/KenanRicky/docker-compose-project.git"


# Boot and Provision the VM
 Create a vagrant Environment from a Vagrant Box.<br/>
 In this case, I am using Ubuntu/jammy64 image.<br/>
 "vagrant box add Ubuntu/jammy64".<br/>
 Run vagrant box list to confirm if the box exists in your VM list.<br/>
 Use "vagrant init" to create the environment<br/>
 "Vagrant Up" to start up the Virtual Machine.<br/>
 You can verify that the VM is running correctly by SSHing into it.<br/>

 # Create Ansible Files and Directories
 The files include:
 1. ansible.cfg
 2. roles
 3. playbook.yaml
 4. inventory.yaml
 5. hosts

Note:
Ignore the .vagrant directory to avoid looping into it in every provision made.<br/>
 
## hosts
This is an inventory where all the VM machines are listed using their IP addresses and other connectivity avenues, like ports.<br/>
127.0.0.1 ansible_port 2222

## ansible.cfg
This is where the defaults are declared.

[defaults]

inventory = hosts.
remote_user = vagrant.
private_key_file = .vagrant/machines/default/virtualbox/private_key.

## playbook.yaml
This is where the commands that are to be executed on the server get declared.<br/>
NOTE: The provision must be defined in the vagrant file by adding the line.<br/>
"config.vm.provision "ansible" do |ansible|
  ansible.playbook = "playbook.yaml
  end"
  at the very end.

  ## roles
  This is where related tasks are grouped to ensure good practice.<br/>
  Roles are created using ansible-galaxy.
  All tasks are defined in the roles.
  docker-installation – Installs Docker and Docker Compose.
  frontend-deployment – Pulls/builds and runs the React frontend container.
  backend-deployment – Pulls/builds and runs the backend Node.js container.
  setup-mongodb - Sets up Mongodb.
  docker-install - Installs Docker to the VM.

 # Vagrant Provision
 This is will give the connectivity to the virtual machine.
In case of any error,
You'll be able to provision while debugging until all goes successful!

