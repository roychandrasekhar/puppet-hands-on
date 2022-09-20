**Install Nginx and MySql Server using Puppet**


Install / Setup Puppet cluster

URL

-----

<u>In Puppet Master</u>

In path : /etc/puppet/code/environments/production/
Create folder as below shown below
├─ manifests/
│   └─ site.pp
└─ modules/
` ` └─ nginxandmysql/
` ` ` ` ` `└─ manifests/
` ` ` ` ` ` ` ` ` `└─ init.pp

Create file  ----------

vi /etc/puppet/code/environments/production/modules/nginxandmysql/manifests/init.pp

```
class nginxandmysql{
    $packages = ['nginx','mysql-server']
    package {$packages:
        ensure => installed,
    }
}
```
![](https://i.imgur.com/DD9IiWg.png)

Create file  ----------
vi /etc/puppet/code/environments/production/manifests/site.pp
```
node default {
    include nginxandmysql
}
```
![](https://i.imgur.com/5J3m4oP.png)

----

In Slave
puppet agent --test
![](https://i.imgur.com/gfHRDwN.png)

Check the mysql and nginx service
![](https://i.imgur.com/A0DZBad.png)
![](https://i.imgur.com/d1WZvtF.png)

