http://99.99.99.98:8080/

docker run --name mynginx -p 8080:80 -v /dockers/nginx_home:/usr/share/nginx/html:rw -d nginx

firewall-cmd --zone=public --add-port=8080/tcp --permanent
firewall-cmd --reload

sudo lsof -i -P -n
sudo lsof -i -P -n | grep LISTEN


docker exec -it mynginx /bin/bash

/usr/share/nginx/html
cat /etc/nginx/nginx.conf

```bash
mv /usr/local/tomcat/webapps /usr/local/tomcat/webapps2
mv /usr/local/tomcat/webapps.dist /usr/local/tomcat/webapps
catalina.sh run
```