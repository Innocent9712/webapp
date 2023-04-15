## Setting up jenkins for ubuntu
### Manual installation


t2.medium - min requirement
ubuntu 20.04


sudo apt update

java -version

sudo apt install default-jre -y

java -version

sudo apt install default-jdk -y

javac -version

sudo apt install software-properties-common

sudo add-apt-repository ppa:linuxuprising/java

sudo apt update

sudo apt install oracle-java11-installer-local

sudo dpkg --configure -a

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -

sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

sudo apt update

`An error would pop up fix it with this`

`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <the key>`

sudo apt update

sudo apt install jenkins -y

sudo systemctl start jenkins

sudo systemctl status jenkins


## Setting up jenkins via Docker
### Install Docker

curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

Now you either implement rootless docker usage
  
```bash
sudo sh -eux <<EOF
# Install newuidmap & newgidmap binaries
apt-get install -y uidmap
EOF
```

dockerd-rootless-setuptool.sh install

or add sudoer user to docker group

sudo usermod -aG docker $USER

> Note:
> Also add the jenkins user to the docker group so jenkins has the permission to use docker
> `sudo usermod -aG docker jenkins`

  
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts

Another thing to note:

> Q: do shell commands specified in a jenkins pipeline that are supposed to run in the host machine work if jenkins was setup as a container?

> A: By default, shell commands in a Jenkins pipeline run inside a Docker container. This means that if you want to execute shell commands on the host machine from a Jenkins pipeline, you need to use a Docker image that has access to the Docker socket on the host machine. This is typically achieved by mounting the Docker socket as a volume when running the Jenkins container.
>
> So if you set up Jenkins as a container and mount the Docker socket as a volume, then you can run shell commands on the host machine from a Jenkins pipeline. However, you should exercise caution when doing so as it can potentially compromise the security of the host machine.

https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04
https://www.ionos.com/digitalguide/server/configuration/install-java-on-ubuntu/
https://stackoverflow.com/questions/57208665/oracle-jdk-11-error-occuring-every-time-i-install-anything-in-terminal
https://askubuntu.com/questions/660599/i-am-installing-jenkins-server-but-its-giving-w-gpg-error


