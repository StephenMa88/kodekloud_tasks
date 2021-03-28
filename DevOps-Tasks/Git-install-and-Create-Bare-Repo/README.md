# Problem
The Nautilus development team shared requirements with the DevOps team regarding new application development.—specifically, they want to set up a Git repository for that project. Create a Git repository on Storage server in Stratos DC as per details given below:

* Install git package using yum on Storage server.
* After that create a bare repository /opt/blog.git (make sure to use exact name).

# Solution
sudo yum install -y git

sudo mkdir /opt/blog.git

cd /opt/blog.git

sudo git init --bare

![image](https://user-images.githubusercontent.com/29349049/112770019-5ca62680-8fd9-11eb-8030-815458f9b9a5.png)

![image](https://user-images.githubusercontent.com/29349049/112770020-5fa11700-8fd9-11eb-8dda-67dd3523627b.png)


Ref: https://saraford.net/2017/03/03/how-to-create-your-own-local-git-remote-repo-thats-not-hosted-on-a-git-server-bare-option-062/
