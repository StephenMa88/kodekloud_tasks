# Problem
There are directory structures in the Stratos Datacenter that need to be changed, including directories that need to be linked to the default Apache document root. We need to accomplish this task using only Puppet as per the instructions given below:

* Create a puppet programming file demo.pp under /etc/puppetlabs/code/environments/production/manifests directory on puppet master node i.e on Jump Server. Within that define a class symlink and perform below mentioned tasks:
* Create a symbolic link through puppet programming code. The source path should be /opt/data and destination path should be /var/www/html on all Puppet agents i.e on all App Servers.
* Create a blank file blog.txt under /opt/data directory on all puppet agent nodes i.e on all App Servers.

# Solution
vi /etc/puppetlabs/code/environments/production/manifests/demo.pp
class symlink {

### Preferred symlink syntax
```
  file { '/opt/data':
    ensure => 'link',
    target => '/var/www/html',
  }
```
### Create blank file
```
  file { "/opt/data/story.txt":
    ensure  => "present",
  }
}
```
### Validate and Create the link
```
puppet parser validate
puppet apply /etc/puppetlabs/code/environments/production/manifests/demo.pp --noop
```

# Troubleshooting
To reset certs (but not necessary for this exercise because the cert was for root user so make sure login as root after ssh in)
```
puppetserver ca clean --certname stapp01.stratos.xfusioncorp.com,stapp02.stratos.xfusioncorp.com,stapp03.stratos.xfusioncorp.com
puppet agent -tv
```
On the agent node run, to test add in --noop
without --noop, puppet agent will run the pull request
```
puppet agent -tv --noop
```

Ref: https://www.puppetcookbook.com/posts/creating-a-symlink.html  https://lzone.de/cheat-sheet/Puppet
