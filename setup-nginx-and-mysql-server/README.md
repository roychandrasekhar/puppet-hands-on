**Install Nginx and MySql Server using Puppet**

Install / Setup Puppet cluster</br>
[Setup Puppet cluster in Ubuntu](https://github.com/roychandrasekhar/puppet-hands-on/tree/main/setup-puppet-cluster)

-----

<u><b>In Puppet Master node</b></u>

In path : /etc/puppet/code/environments/production/ </br>
Create folder as below shown below
```
├─ manifests/
│   └─ site.pp
└─ modules/
    └─ nginxandmysql/
         └─ manifests/
             └─ init.pp
```

Create file  ---------- </br>
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

Create file  ---------- </br>
vi /etc/puppet/code/environments/production/manifests/site.pp
```
node default {
    include nginxandmysql
}
```
![](https://i.imgur.com/5J3m4oP.png)

----

<u><b>Now in Slave node </b></u></br>
<span style="color:blue;font-weight:bold"># puppet agent --test</span></br>
![](https://i.imgur.com/gfHRDwN.png)

Check the mysql and nginx service</br>
![](https://i.imgur.com/A0DZBad.png)</br>

Check in browser also
![](https://i.imgur.com/d1WZvtF.png)

