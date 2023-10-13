# aws-jenkins

# How to Install jenkins (aws ubuntu server)

1. ### Select ubuntu image

![Alt text](/images/image-0.png)

2. ### Select instance type

![Alt text](/images/image-1.png)

3. ### Select ubuntu key for ssh

![Alt text](/images/image-2.png)

4. ### For the network setting make sure it has port 8080 is available. Because jenkins runs on port 8080

![Alt text](/images/image-3.png)

5. ### Click launch

![Alt text](/images/image-4.png)

6. ### Copy the ssh command and paste it in your terminal

![Alt text](/images/image-5.png)

7. ### Copy paste below command to update the repository in the machine and install jenkins

```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

```
sudo apt-get update
```

```
sudo apt-get install jenkins
```

8. ### Make sure java installed

- To check java installed

```
java -v
```

- To install java

```
sudo apt update
sudo apt install openjdk-17-jre
java -version
openjdk version "17.0.7" 2023-04-18
OpenJDK Runtime Environment (build 17.0.7+7-Debian-1deb11u1)
OpenJDK 64-Bit Server VM (build 17.0.7+7-Debian-1deb11u1, mixed mode, sharing)
```

9. ### Start Jenkins

- To check jenkins status

```
sudo systemctl status jenkins
```

- To start jenkins service

```
sudo systemctl start jenkins
```

> ![Alt text](/images/image-6.png)

- should see the status active

10. ### To check the password for the jenkins

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

- copy paste the Administrator password

![Alt text](/images/image-7.png)

# Install jenkins using docker

- use the Dockerfile provided

```
docker build -t myjenkins-blueocean:2.414.2-1 .
```

- to run the image

```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8081:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.414.2-1
```

- to access docker container

```
docker exec -it jenkins-blueocean bash
```

- to access docker container as root

```
docker exec -it -u root jenkins-blueocean bash
```

# Resources

- <a href="https://www.jenkins.io/doc/book/installing/linux/#debianubuntu">Jenkins Installation</a>
- <a href="https://www.jenkins.io/doc/book/installing/docker/">Jenkins Installation using docker</a>
