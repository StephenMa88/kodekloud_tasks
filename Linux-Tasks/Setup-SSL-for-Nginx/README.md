# Problem
The system admins team of xFusionCorp Industries needs to deploy a new application on App Server 2 in Stratos Datacenter. They have some pre-requites to get ready that server for application deployment. Prepare the server as per requirements shared below:
* Install and configure nginx on App Server 2.
* On App Server 2 there is a self signed SSL certificate and key present at location /tmp/nautilus.crt and /tmp/nautilus.key. Move them to some appropriate location and deploy the same in Nginx.
* Create an index.html file with content Welcome! under Nginx document root.
* For final testing try to access the App Server 2 link (either hostname or IP) from jump host using curl command. For example curl -Ik https://<app-server-ip>/.

# Solution
```
sudo yum install -y epel-release && sudo yum install -y nginx
sudo mkdir -p /etc/pki/nginx/private
sudo mv /tmp/nautilus.crt /etc/pki/nginx/nautilus.crt
sudo mv /tmp/nautilus.key /etc/pki/nginx/private/nautilus.key
```
sudo vi /etc/nginx/nginx.conf
```
ssl_certificate "/etc/pki/nginx/nautilus.crt";
ssl_certificate_key "/etc/pki/nginx/private/nautilus.key";
```
```
mkdir -p /usr/share/doc/HTML
```
sudo vi /usr/share/doc/HTML/index.html
```
<h1>Welcome!</h1>
```

Ref:
* https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-on-centos-7
* https://kifarunix.com/configure-nginx-with-ssl-tls-certificates-on-centos-8/
