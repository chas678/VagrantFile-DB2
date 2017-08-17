VagrantFile-DB2
===============
This vagrant file installs an IBM DB2 express-c 9.7 onto an Ubuntu 10.04 Lucid box.
Install Virtualbox and Vagrant first
* http://virtualbox.org
* http://www.vagrantup.com
x

## running
Execute vagrant up in the directory with the Vagrantfile and provision.sh - it'll take a while first time.  Subsequent times will take about 30 seconds.
vagrant halt to stop it.
Box is set to be on private network IP 192.168.56.70
Keep the guest additions up to date in Virtualbox by using Vagrant plugin:
	vagrant plugin install vagrant-vbguest


## whitepaper
Canonical Ubuntu and DB2 Install info and whitepaper see: http://public.dhe.ibm.com/software/dw/db2/express-c/whitepaper/DB2andUbuntuWhitepaper.pdf

## machine logins

* User: vagrant
* Password: vagrant
* Root password: vagrant
* Database (and machine user)
* user: db2inst1
* password: db2inst1

## database install
* DB2 Express-C Edition 9.7 Fix Pack 5 for Linux x86_64 has been installed in /opt/ibm/db2/V9.7.
* The following DAS user has been configured:  dasusr1
* The following instances (and user) have been configured: db2inst1
* sample database is installed by running db2sample (in provisioning script) - see http://pic.dhe.ibm.com/infocenter/db2luw/v9r7/index.jsp?topic=%2Fcom.ibm.db2.luw.admin.cmd.doc%2Fdoc%2Fr0001934.html
* To remove SAMPLE database:
```
  vagrant ssh
  sudo su - db2inst1
  db2 drop database sample
```
* For more details, consult DB2 Information Center: http://publib.boulder.ibm.com/infocenter/db2luw/v9r7

DB2 network ports can be seen by viewing: cat /etc/services:

```
		db2c_db2inst1         50000/tcp
		# FCM port information
		DB2_db2inst1          60000/tcp
		DB2_db2inst1_1        60001/tcp
		DB2_db2inst1_2        60002/tcp
		DB2_db2inst1_END      60003/tcp
```

## JDBC connections
* use latest DB2 JDBC driver (10.5) - they are backwards compatible
* JDBC connection URL can have extra properties see: http://pic.dhe.ibm.com/infocenter/db2luw/v10r5/index.jsp?topic=%2Fcom.ibm.db2.luw.apdv.java.doc%2Fsrc%2Ftpc%2Fimjcc_rjvdsprp.html

###Examples:
* (Note VirtualBox port forwarding is on so either the private network or localhost will work)
* jdbc:db2://localhost:50000/sample  password: db2inst1
* jdbc:db2://192.168.56.70:50000/sample password: db2inst1

