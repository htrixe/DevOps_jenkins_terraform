#  Build Jenkins Docker Agents II - Commands
$ sudo systemctl disable firewalld

$ sudo systemctl enable --now docker

$ sudo usermod -aG docker jenkins

$ sudo chmod 666 /var/run/docker.sock



## Execute Jenkins Docker --

- docker run -d -u root --privileged=true --volume /root/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 -p 50000:50000 --name jenkins-centos jenkins/jenkins:lts

----