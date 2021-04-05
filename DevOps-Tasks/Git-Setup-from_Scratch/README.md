# Problem
Some new developers have joined xFusionCorp Industries and have been assigned Nautilus project. They are going to start development on a new application, and some pre-requisites have been shared with the DevOps team to proceed with. Please note that all tasks need to be performed on storage server in Stratos DC.

a. Install git, set up any values for user.email and user.name globally and create a bare repository /opt/official.git.

b. There is an update hook (to block direct pushes to master branch) under /tmp on storage server itself; use the same to block direct pushes to master branch in /opt/official.git repo.

c. Clone /opt/official.git repo in /usr/src/kodekloudrepos/official directory.

d. Create a new branch xfusioncorp_official in repo that you cloned in /usr/src/kodekloudrepos.

e. There is a readme.md file in /tmp on storage server itself; copy that to repo, add/commit in the new branch you created, and finally push your branch to origin.

f. Also create master branch from your branch and remember you should not be able to push to master as per hook you have set up.

# Solution

ssh natasha@ststor01

## task a
```
sudo yum install -y git
sudo git config --global user.name root
sudo git config --global user.email root@ststor01.stratos.xfusioncorp.com
```
## task b
```
cd /opt
sudo git init --bare official.git
sudo cp /tmp/update official.git/hooks/.
```
## task c
```
cd /opt
sudo git clone official.git /usr/src/kodekloudrepos/official
```
## task d
```
cd /usr/src/kodekloudrepos/official
sudo git checkout -b xfusioncorp_official
```
## task e
```
sudo cp /tmp/readme.md .
sudo git add --all
sudo git commit -m "add readme"
sudo git push origin xfusioncorp_official
```
## task f
```
sudo git checkout master
sudo touch test-file
sudo git add --all
sudo git commit -m "test if master can checkin"
sudo git push origin master
```
You will get an error message as seen below



# Ref
- https://stackoverflow.com/questions/7632454/how-do-you-use-git-bare-init-repository
- https://stackoverflow.com/questions/9162271/fatal-not-a-valid-object-name-master/9162347


