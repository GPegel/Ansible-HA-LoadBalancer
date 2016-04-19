# Ansible-HA-LoadBalancer
High-Availability Load Balancer with ‘HAProxy’.

# What does this playbook do?
When you need a quick way to setup a load balancer and multiple end-points for serving websites then this playbook could be a great help. In my example I've used 6 servers in total. One server as a load balancer and 4 servers as end-points and 1 extra server as a fallback for the 4 end-points. The load balancer will be running HAProxy (version 1.5.14) and a small statistics report is included.

# Which roles will be installed?
All roles will be installed including their configuration files where needed.

1. Apache
2. Firewall
3. HAProxy
4. Common*

The 'Common' role I've created is for getting YUM configured, installing the EPEL-Release repository and configuring NTP servers.

# How to start the playbook?

At first be sure that all your servers are up & running and they have your local SSH keys.
In my case I started the 'common.yml' playbook first and after that I started the 'site.yml' playbook.

1.
```
$ ansible-playbook common.yml -i environments/production -e env=environments/production -u root
```

2.
```
$ ansible-playbook site.yml -i environments/production -e env=environments/production -u root
```

# How to see if the load balancer works?
Enter the IP address of your load balancer into a browser. If everything went well, you will see a small website.


```
$ http://ip-address
```
To open the HA Proxy statistics page please go to this URL:
The credentials are 'admin/admin' and you can change this in "/roles/haproxy/templates/haproxy.cfg.j2"
```
$ http://ip-address:8080/haproxy?stats
```

# Extra information

1. Ansible version 2.0.1.0
2. Playbook has been tested on virtual CentOS 7 servers
3. Host: Ubuntu version 15.10

This playbook is created by me, myself and I   ;-)
