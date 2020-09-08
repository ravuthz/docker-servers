## Tomcat 9.0

### Build & Up Tomcat
```bash
docker-compose -f ./tomcat/docker-compose.yml up -d --build --force-recreate

docker exec -it mytomcat bash
docker exec -it mytomcat sh -c "ls /usr/local/tomcat/webapps"

docker restart mytomcat
docker port mytomcat
docker logs mytomcat

docker-compose logs mytomcat
```

### Build & Up Jenkins
```bash
# docker run --name myjenkins -d -p 8080:8080 jenkinsci/blueocean \
# --env JAVA_OPTS="-Xmx8192m" --env JENKINS_OPTS="--handlerCountMax=300"

docker-compose -f ./jenkins/docker-compose.yml up -d --build --force-recreate

docker exec -it myjenkins bash
# /var/jenkins_home/secrets/initialAdminPassword

docker exec -it myjenkins sh -c "cat /var/jenkins_home/secrets/initialAdminPassword"
cat /root/dockers/jenkins/data/secrets/initialAdminPassword

docker exec -it myjenkins sh -c "echo $JENKINS_URL"

# JENKINS_URL/jnlpJars/jenkins-cli.jar
http://178.128.63.60:8080/jnlpJars/jenkins-cli.jar

# JENKINS_URL/user/USERNAME/configure
http://178.128.63.60:8080/user/adminz/configure

cd D:/
http://178.128.63.60:8080/cli/
java -jar jenkins-cli.jar -s http://178.128.63.60:8080/ -webSocket help
java -jar jenkins-cli.jar -s http://178.128.63.60:8080/ -webSocket who-am-i
java -jar jenkins-cli.jar -s http://178.128.63.60:8080/ build job-name


http://178.128.63.60:8080/
adminz / 123123


### Jenkins list plugins
http://178.128.63.60:8080/systemInfo
https://stackoverflow.com/questions/9815273/how-to-get-a-list-of-installed-jenkins-plugins-with-name-and-version-pair
### Jenkins scripts
https://www.jenkins.io/doc/book/managing/script-console/
http://178.128.63.60:8080/script
```

#### Allow Port
```bash
# Centos - allow port 8080
firewall-cmd --zone=public --add-port=8080/tcp --permanent
firewall-cmd --reload

lsof -i -P | grep http
lsof -i -P | grep postgres
lsof -i -P | grep docker
lsof -i -P | grep LISTEN

# Ubuntu - allow port 8080
sudo ufw status verbose
sudo ufw allow 8080/tcp
```




<!-- https://ravuthz@bitbucket.org/local-projects/micro-fin-admin.git -->

## Jenkins Docker
https://technology.riotgames.com/news/putting-jenkins-docker-container
https://technology.riotgames.com/news/docker-jenkins-data-persists
https://dev.to/andresfmoya/install-jenkins-using-docker-compose-4cab

## Angular Nginx Docker
http://178.128.63.60:8080/
```bash
```


http://178.128.63.60:8080/cli/
http://178.128.63.60:8080/env-vars.html/
```bash

```


 - spring.datasource.url=jdbc:postgresql://srv_iloan_db:5432/i_loan


mvn -pl core,i-collector clean package -Pproduction -T 1C -Dmaven.test.skip=true -Dspring.profiles.active=prd

<!-- spring.profiles.active -->

java -jar i-collector/target/i-collector-2.0-SNAPSHOT.war -Dspring.profiles.active=prd