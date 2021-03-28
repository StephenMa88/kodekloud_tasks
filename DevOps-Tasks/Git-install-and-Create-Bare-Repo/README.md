# Problem
The Nautilus development team shared requirements with the DevOps team regarding new application development.—specifically, they want to set up a Git repository for that project. Create a Git repository on Storage server in Stratos DC as per details given below:


Install git package using yum on Storage server.

After that create a bare repository /opt/blog.git (make sure to use exact name).

# Solution
sudo yum install git

sudo mkdir /opt/blog.git

cd /opt/blog.git

sudo git init --bare


Ref: https://saraford.net/2017/03/03/how-to-create-your-own-local-git-remote-repo-thats-not-hosted-on-a-git-server-bare-option-062/
