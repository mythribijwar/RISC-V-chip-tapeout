WSL Setup → Docker Install → OpenLane Build → Ready to Design

1.WSL SETUP

Step 1: Enable WSL

Open PowerShell as Administrator and run:

        wsl --install
Step 2: Complete Setup

Restart your system when prompted.

Update your package list:

    sudo apt-get update
    sudo apt-get upgrade

2..DOCKER SETUP

Installing Docker

Purpose: Docker provides containerized environment for OpenLane tools.

   
     sudo apt-get update
     sudo apt-get install ca-certificates curl
     sudo install -m 0755 -d /etc/apt/keyrings
     sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
     sudo chmod a+r /etc/apt/keyrings/docker.asc


    echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo \"$VERSION_CODENAME\") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
Install Docker Engine

    sudo apt-get install docker-ce docker-ce-cli containerd.ioVerify Installation

Add Your User to the Docker Group

    sudo groupadd docker
    sudo usermod -aG docker $USER
    sudo reboot
    
Run the test image

  after reboot

     sudo docker run hello-world

3..OPENLANE SETUP

Verify Prerequisites

    git --version
    docker --version
    python3 --version
    python3 -m pip --version
    make --version
    python3 -m venv -h

Update & Install Required Packages

     sudo apt-get update
     sudo apt-get upgrade
    sudo apt install -y build-essential python3 python3-venv python3-pip python3-tk curl make git
    
Clone and Build OpenLane

    cd $HOME
    git clone https://github.com/The-OpenROAD-Project/OpenLane
    cd OpenLane
    make
    make test

4..VERIFICATION COMANDS

      # Test Docker
     docker --version

     # Test OpenLane
     cd $HOME/OpenLane
     make test



sudo docker run hello-world

