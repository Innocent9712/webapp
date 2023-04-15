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

  
docker run -p 8080:8080 -p 50000:50000 -d -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts



https://www.digitalocean.com/community/tutorials/how-to-install-java-with-apt-on-ubuntu-20-04
https://www.ionos.com/digitalguide/server/configuration/install-java-on-ubuntu/
https://stackoverflow.com/questions/57208665/oracle-jdk-11-error-occuring-every-time-i-install-anything-in-terminal
https://askubuntu.com/questions/660599/i-am-installing-jenkins-server-but-its-giving-w-gpg-error


