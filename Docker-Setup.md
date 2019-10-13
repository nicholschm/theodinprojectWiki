# Running TOP with Docker

Getting started is easy. We just need to:
1. Install Docker & Docker Compose
2. Run the command

# Install Docker and Docker-compose

#### Ubuntu:

Taken from [Docker Documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

```
# Add Docker's GPG key:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# Add the Docker Repository:
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"

# Update and Install
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Add yourself to the docker group
sudo usermod -aG docker $(whoami)
```

Restart your terminal and try `docker version`. You should get a valid output and not require `sudo`

Then download and install Docker-Compose:

Instructions from [Docker Documentation](https://docs.docker.com/compose/install/)

```
# Download the binary
sudo curl \
  -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" \
  -o /usr/local/bin/docker-compose

# Then chmod the binary
sudo chmod +x /usr/local/bin/docker-compose
```


#### MacOS

Simply download and run the Docker app that can be downloaded from [here](https://download.docker.com/mac/stable/Docker.dmg)

[Official Site](https://hub.docker.com/editions/community/docker-ce-desktop-mac)

This app provides both `docker` and `docker-compose`

## Up and running

Simply `cd` into the base directory and run

```
docker-compose up -d
```

This will build all the containers and get everything started for you. After a few minutes you should be able to access http://localhost:3000 on your local browser and see The Odin Project homepage.