Install Puppet cluster environment in Virtual Box

1. Setup 2 Ubuntu machine, one for Master and one for Slave</br>
![](https://i.imgur.com/Znmmhor.png)</br>
![](https://i.imgur.com/2gUvPET.png)

2. Setup IP and open port 8140/TCP for both the machine
* Master
        - ifconfig enp0s8 192.168.56.200 netmask 255.255.255.0
        - ufw allow 8140/tcp
* Slave
        - ifconfig enp0s8 192.168.56.201 netmask 255.255.255.0
        - ufw allow 8140/tcp

3. Add Puppet Master IP in hosts file on each machine as below
192.168.56.200 puppet
![](https://i.imgur.com/IIib4Qr.png)</br>
![](https://i.imgur.com/Ut38wvR.png)

    This must be added with same content in both the Machine’s

4. Puppet Master Setup - Install package and service as super user
apt-get update
wget https://apt.puppetlabs.com/puppet-release-bionic.deb
dpkg -i puppet-release-bionic.deb
apt-get install puppetmaster -y
![](https://i.imgur.com/L8XKP2D.png)</br>
apt policy puppetmaster
systemctl status puppet-master.service
systemctl restart puppet-master.service

5. Puppet slave setup
apt-get update
wget https://apt.puppetlabs.com/puppet-release-bionic.deb
dpkg -i puppet-release-bionic.deb
apt-get install puppet -y
systemctl start puppet.service
systemctl enable puppet.service
systemctl restart puppet.service

6. Certificate signing steps
puppet cert list
puppet cert sign --all
![](https://i.imgur.com/gg8Ke9G.png)
![](https://i.imgur.com/zCz3ygG.png)

7. Connection Testing
Goto Puppet Master ---------------------------------------------</br>
mkdir -p /etc/puppet/code/environments/production/manifests/
vi /etc/puppet/code/environments/production/manifests/site.pp</br>
file {'/tmp/it\_works.txt':</br>
`   `ensure   => present,</br>
`   `mode     => '0644',</br>
`   `content  => "It works on ${ipaddress\_eth01}!\n" </br>
}

    systemctl restart puppet-master.service

    Now in Puppet Slave ---------------------------------------------</br>
puppet agent --test</br>
cat /tmp/it\_works.txt

   ![](https://i.imgur.com/8uFsDDT.png)


