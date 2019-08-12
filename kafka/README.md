Kafka Cluster
=============

Apache Kafka is a high-throughput distributed messaging system that you can use to facilitate scalable data collection. An installation of Apache Kafka consists of a number of brokers that run on individual servers that are coordinated by an instance of Apache ZooKeeper. You can start by creating a single broker and you can add more as you scale your data collection architecture. In the scalable data collection architecture, the Receiver cluster writes data to Apache Kafka topics and partitions, based on the data sources. The Sender cluster reads data from Apache Kafka, does some processing and sends the data to Log Analysis.

Requirements
------------

This Role works on 3 node architecture. User executing this Role must require lists :-
1) Ansible Master Linux VM ( having ansible v2.7 or above) with user having passwordless access on all client machines.
2) Three Linux VMs or Physical machines (clients) having a same user as ansible master server with full sudo access (NOPASSWD: ALL)
3) This Role must be copied inside /etc/ansible/ diectory of master server. Playbook kafka.yml must be in /etc/ansible/ directory and kafka folder must be in /etc/ansible/roles/ directory.
4) Host group kafka must be defined in /etc/ansible/hosts file having all 3 IPs of client machines on which kafka needs to be installed. For example :-

[kafka]
10.X.X.X
10.Y.Y.Y
10.Z.Z.Z

5) Oracle JDK 8 needs to be downloaded and kept inside ./roles/kafka/files/ directory. You can download Oracle JDK 8 from below link :
https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

Role Variables
--------------

This Role has a centralized variable file kept inside ./kafka/vars/main.yml
The yml consists of below variables :
1) nodes : 3 (no. of kafka nodes. In our case it is 3)
2) All 3 IPs of ansible clients needs to be defined as IP1, IP2, IP3 where kafka needs to be installed.
3) java_package: Need to specify the rpm name of the oracle jdk which you have already downloaded.
4) kafka_pkg: Need to define the kafka package name along with its version
5) zookeeper_pkg: Need to define the zookeeper package name along with its version

Dependencies
------------

This Role does not have any kind of dependencies on any other role or playbook.

How to Use this Role
--------------------

Once you have setup above all requirements then simply logon to the Ansible Master server with your specified ansible user and go to directory /etc/ansible/ and run below command :-

<b3>ansible-playbook kafka.yml</b3>

License
-------

No license is required as packages used in the installation are free.

Author Information
------------------

This ansible role has been developed by me (Ali Asgar Attari). In case of any issues you can reach me on ali.attari52@gmail.com
