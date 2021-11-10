---
title: "Cloud"
linkTitle: "Cloud"
weight: 5
description: >
  Run neurodesktop using Oracle or Azure cloud computing
---

## Minimum System Requirements
1. At least 3GB free space for neurodesktop base image
2. Docker requirements. Details found under https://docs.docker.com/get-docker/

## Quickstart
1. Open an SSH connection to your cloud instance with port forwarding
<pre class="language-shell command-line" data-prompt="$">
<code>ssh -L 8080:127.0.0.1:8080 opc@133.71.33.71</code>
</pre>

2. Install Docker from here: https://docs.docker.com/get-docker/ 

### RHEL/CentOS (yum-based)
Refer to https://docs.docker.com/engine/install/centos/

One example to install docker in a yum-based distribution could look like this:
<pre class="language-shell command-line" data-prompt="$">
<code>sudo dnf install -y yum-utils 
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io
sudo systemctl enable docker
sudo systemctl start docker
sudo docker version
sudo docker info
sudo groupadd docker
sudo usermod -aG docker $USER
sudo chown root:docker /var/run/docker.sock
newgrp docker</code>
</pre>

### Ubuntu/Debian (apt-based)
Refer to https://docs.docker.com/engine/install/ubuntu/

One example to install docker in a apt-based distribution could look like this:
<pre class="language-shell command-line" data-prompt="$" data-output="5">
<code>sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io</code>
</pre>

3. Create a local folder where the downloaded applications will be stored, e.g. ~/neurodesktop-storage

4. Open a terminal, and type the folowing command to automatically download the neurodesktop container and run it (Mac, Windows, Linux commands listed below) 

<pre class="language-shell command-line" data-prompt="$" data-output="2-9">
<code>sudo docker run \
  --shm-size=1gb -it --privileged --name neurodesktop \
  -v ~/neurodesktop-storage:/neurodesktop-storage \
  -e HOST_UID="$(id -u)" -e HOST_GID="$(id -g)" \
  -p 8080:8080 -h neurodesktop-{{< params/neurodesktop/version >}} \
  vnmd/neurodesktop:{{< params/neurodesktop/version >}}</code>
</pre>
<!-- neurodesktop version found in neurodesk.github.io/data/neurodesktop.toml -->

(notice: if you get errors in neurodesktop then check if the ~/neurodesktop-storage directory is writable to all users, otherwise run `chmod a+rwx ~/neurodesktop-storage`)

5. Once neurodesktop is downloaded i.e. `guacd[77]: INFO:        Listening on host 127.0.0.1, port 4822` is displayed in terminal, open a browser and go to:
```
http://localhost:8080/#/?username=user&password=password
```
or open a VNC Client and connect to port 5901 (for this -p 5901:5901 has to be added to the docker call)

6. neurodesktop is ready to use!
- User is `user`
- Password is `password`

## Stopping neurodesktop:
When done processing your data it is important to stop and remove the container - otherwise the next start or container update will give an error ("... The container name "/neurodesktop" is already in use...")
1. Click on the terminal from which you ran neurodesktop

2. Press Ctrl-C

3. Run:
<pre class="language-shell command-line" data-prompt="$">
<code>sudo docker stop neurodesktop && sudo docker rm neurodesktop</code>
</pre>

## Portforwarding to an iOS ipad 
You can also connect to this cloud instance from your iOS device :) For this install https://webssh.net/documentation/help/networking/port-forwarding/ and create a tunnel (the tool is free for one connection). Start the docker container in a screen session and then connect to it from your ios device in the browser.

## Cloud-provider specific Tutorials 
| Cloud provider | link                                                                                    |
|----------------|-----------------------------------------------------------------------------------------|
| Oracle         | https://mri.sbollmann.net/index.php/2020/12/08/run-neurodesk-on-oracle-cloud-free-tier/ |
| Azure          | https://henryjburg.medium.com/neurodesk-running-on-azure-3e38c590a152                   |