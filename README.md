# aws-jenkins installation

<details style='color:#FF9900; font-size: 1.5rem'>
  <summary>
    <h2?> How to Install jenkins (aws ubuntu server)</h2>
  </summary>

1. ### Select Preferred image Select instance type

![Alt text](/images/image-1.png)

2. ### Select ubuntu key for ssh

![Alt text](/images/image-2.png)

3. ### For the network setting make sure it has port 8080 is available. Because jenkins runs on port 8080

![Alt text](/images/image-3.png)

3. ### Click launch

![Alt text](/images/image-4.png)

4. ### Copy the ssh command and paste it in your terminal

![Alt text](/images/image-5.png)

5. ### Copy paste below command to update the repository in the machine and install jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null
```

```bash
sudo apt-get update
```

```bash
sudo apt-get install jenkins
```

6. ### Make sure java installed

- To check java installed

```bash
java -v
```

- To install java

```bash
sudo apt update
sudo apt install openjdk-17-jre
java -version
openjdk version "17.0.7" 2023-04-18
OpenJDK Runtime Environment (build 17.0.7+7-Debian-1deb11u1)
OpenJDK 64-Bit Server VM (build 17.0.7+7-Debian-1deb11u1, mixed mode, sharing)
```

7. ### Start Jenkins

- To check jenkins status

```sh
sudo systemctl status jenkins
```

- To start jenkins service

```bash
sudo systemctl start jenkins
```

![Alt text](/images/image-6.png)

- should see the status active

8. ### To check the password for the jenkins

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

- copy paste the Administrator password

![Alt text](/images/image-7.png)

</details>

<details open style='color:#6ca3eb; font-size: 1.5rem'>

  <summary>Install jenkins using docker</summary>


- use the Dockerfile provided

```bash
docker build -t myjenkins-blueocean:2.414.2-1 .
```

- to run the image

```bash
docker run --name jenkins-blueocean --restart=on-failure --detach \
--network jenkins --env DOCKER_HOST=tcp://docker:2376 \
--env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
--publish 8081:8080 --publish 50000:50000 \
--volume jenkins-data:/var/jenkins_home \
--volume jenkins-docker-certs:/certs/client:ro \
myjenkins-blueocean:2.414.2-1
```

- to access docker container

```bash
docker exec -it jenkins-blueocean bash
```

- to access docker container as root

```bash
docker exec -it -u root jenkins-blueocean bash
```

</details>

## Resources

  <!-- - <a href="https://www.jenkins.io/doc/book/installing/linux/#debianubuntu">Jenkins Installation</a> -->

- [Jenkins Installation](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)

  <!-- - <a href="https://www.jenkins.io/doc/book/installing/docker/">Jenkins Installation using docker</a> -->

- [Jenkins Installation using docker](https://www.jenkins.io/doc/book/installing/docker/)
