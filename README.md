# Employee Recognition Platfrom

### Required software

#### Docker 

Docker is a containerization technology that allows you to run (containers)[https://www.docker.com/resources/what-container#:~:text=A%20Docker%20container%20image%20is,tools%2C%20system%20libraries%20and%20settings.] locally. We are going to run our database as a container. 

1 Update system repositories.
```
sudo apt-get update
```
2 Install required libraries.
```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
3 Add the official docker GPG keys that allow you to verify that your installation of docker is valid and can be safely used. Never install software which validity and safety can not be guaranteed and verified.
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
4 Setup the stable docker repository.
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
5 Update system repositories.
```
sudo apt-get update
```
6 Install docker.
```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

#### Docker Compose

Docker only allows you to run and manipulate the containers one at a timne. This gets tedious and time consuming. Docker Compose allows you to define how you would like your containers to function (memory and cpu limits, ports, volumes, networking, env variables, etc). as code isnside the docker-compose.yml file. Without it you would have to setup manually each container using several commands every time you need to use it. 

1 Create a directory for docker plugins.
```
mkdir -p ~/.docker/cli-plugins/
```
2 Download the docker-compose plugin from official repository.
```
curl -SL https://github.com/docker/compose/releases/download/v2.2.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
```
3 Make the plugin executable.
```
chmod +x ~/.docker/cli-plugins/docker-compose
```
4 Allow the current user to use docker-compose even if not root.
```
sudo chown $USER /var/run/docker.sock
```
5 Verify installation.
```
docker compose version
```


#### RVM (Ruby Version Manager)

This is the software that allows us to use different versions of Ruby. Different project require different versions of Ruby and this allows for seamless switching between versions and gemsets.

1 Update the system repositories.
```
sudo apt update
```
2 Install the dependencies required for ruby to funcion properly.
```
sudo apt install curl g++ gcc autoconf automake bison libc6-dev libffi-dev libgdbm-dev libncurses5-dev libsqlite3-dev libtool libyaml-dev make pkg-config sqlite3 zlib1g-dev libgmp-dev libreadline-dev libssl-dev
```
3 Add the RVM GPG keys. 
```
gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```
4 Install RVM
```
curl -sSL https://get.rvm.io | bash -s stable
```
5 Reload the script envionment variables. Your shell doesn't know yet that you installed a new program.
```
source ~/.rvm/scripts/rvm
6 Verify that RVM is installed and working. The following line should return a version number.
```
rvm -v
```

#### Ruby
```
1 Install Ruby 3.0.2 (modern but not bleeding edge).
``` 
rvm install 3.0.2
```
2 Confirm installation is complete
Running this command should print out the version of Ruby you have installed.
```
ruby -v
```
3 Set Ruby 3.0.2 as the default version of Ruby.
```
rvm default 3.0.2
```

#### NVM (Node Version Manager)

This is a tool similar to RVM but for Node.js. It allows us to use different versions of Node.js.

1 Install NVM
In this step you are running a raw file file but it comes from a verified source, the creators of NVM. Feel free to confirm (here)[https://github.com/nvm-sh/nvm#install--update-script]
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
2 Reload the shell environment variables.
```
source ~/.bashrc

```
3 Verify that NVM is installed and working. The following line should return a version number.
```
nvm -v 
```

#### Node.js
1 Install the required version of Node.js.
```
nvm install 14.18.0
```
2 Set the required version of Node.js as the default version of Node.js.
```
nvm alias default 14.18.0
```
3 Verify that Node.js is installed and working. The following line should return a version number.
```
node -v
```

#### PostreSQL dependencies

Postgres is the database that we are going to use for development. It has some system specific dependencies that we need to install. Even though we are running it as a non-root user, we need to install these dependencies locally.

1 Install the dependencies required for Postgres to function properly.
```
apt-get update && apt-get install -y build-essential libpq-dev
```

### Setup

1 Start a new terminal window for this command. Start the docker database contaier.
```
docker-compose up  
```
2 Run the setup script. It can take several minutes to complete.
```
bin/setup
```

### How to start the app
```
rails server
```
