#  Build Jenkins Docker Agents II - Commands
$ sudo systemctl disable firewalld

$ sudo systemctl enable --now docker

$ sudo usermod -aG docker jenkins

$ sudo chmod 666 /var/run/docker.sock



## Execute Jenkins Docker --

- docker run -d -u root --privileged=true --volume /root/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 -p 50000:50000 --name jenkins-centos jenkins/jenkins:lts

----

## I faced the following issue. I fixed the issue by applying
mountPath: /etc/nginx/nginx.conf
subPath: nginx.conf

- root@K8Single ~/pods_and_containers# kubectl get pods -o wide
NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES
configmap-env-demo 1/1 Running 43 43h 172.17.0.4 k8single
configmap-posix-demo 1/1 Running 0 20h 172.17.0.6 k8single
configmap-vol-demo 1/1 Running 20 20h 172.17.0.5 k8single
nginx-pod 0/1 CrashLoopBackOff 1 3s 172.17.0.7 k8single
root@K8Single ~/pods_and_containers# kubectl get logs nginx-pod
error: the server doesn't have a resource type "logs"
root@K8Single ~/pods_and_containers [1]# kubectl logs nginx-pod
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: error: /etc/nginx/conf.d/default.conf is not a file or does not exist
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2021/07/08 07:38:55 [emerg] 1#1: open() "/etc/nginx/mime.types" failed (2: No such file or directory) in /etc/nginx/nginx.conf:29
nginx: [emerg] open() "/etc/nginx/mime.types" failed (2: No such file or directory) in /etc/nginx/nginx.conf:29

---

