# Tristana Docker
Docker deployment

# Installation

## Install Docker / Git
https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/

## Install Docker Compose
https://docs.docker.com/compose/install/#install-compose


## Install Tristana

Create a /var/tristana folder, clone the Official Skylark Docker Image into it:

```bash
mkdir /var/tristana
git clone https://github.com/GreenNerd/tristana-docker.git /var/tristana
cd /var/tristana
```
Build it manually
```bash
cd /var/tristana/images/base && ./build
cd /var/tristana/images/production && ./build
```

Run!

```bash
cd /var/tristana
docker-compose up -d
```

Before run you might run below:
```bash
cd /var/tristana
./script/install # First install, precompile assets
./script/start # Run server
./script/update # Update container
```
