
# Kafka role

This role will install Apache Kafka which consists of a number of brokers that run on individual servers that are coordinated by an instance of Apache ZooKeeper. 

You can start by creating a single broker and you can add more as you scale your data collection architecture. 

The Receiver cluster writes data to Apache Kafka topics and partitions based on the data sources. 

The Sender cluster reads data from Apache Kafka and performs processing and sends the data to Log Analysis.

## Requirements

This Role works on 3 node architecture. User executing this Role must require lists :-
1) Ansible Master Linux VM ( having ansible v2.7 or above) with user having passwordless access on all client machines.
2) Three Linux VMs or Physical machines (clients) having a same user as ansible master server with full sudo access (NOPASSWD: ALL)
3) Host group kafka must be defined in the inventory/hosts file having all 3 IPs of client machines on which kafka needs to be installed. 
For example, hosts.yml:
```yaml
all:
  children:
    kafka:
      10.X.X.X: {}
      10.Y.Y.Y: {}
      10.Z.Z.Z: {}
      
```

## Role Variables

This Role has a centralized variable file kept inside ./kafka/vars/main.yml
The yml consists of below variables :
1) bootstrap_kafka__num_nodes : 3 (no. of kafka nodes. In our case it is 3)
2) All 3 IPs of ansible clients needs to be defined as bootstrap_kafka__ip(1,2,3) where kafka needs to be installed.
3) bootstrap_kafka__java_packages: Need to specify the rpm name of the oracle jdk which you have already downloaded.
4) bootstrap_kafka__kafka_pkg: Need to define the kafka package name along with its version
5) bootstrap_kafka__zookeeper_pkg: Need to define the zookeeper package name along with its version

## Dependencies

This Role does not have any kind of dependencies on any other role or playbook.

## How to Use this Role

This Role has been tested and working fine on Centos-7 & Redhat-7 machines

1) Install Ansible on Master - yum install ansible

2) Uncomment inventory line in ansible.cfg

test/ansible.cfg:
```ini
inventory = /etc/ansible/hosts
```

3) Enter kafka client hosts IP in hosts file

test/hosts.yml:
```yaml
all:
  children:
    kafka:
      10.X.X.X: {}
      10.Y.Y.Y: {}
      10.Z.Z.Z: {}
      
```

Replace the IP with your client machines IP


4) run below command

```shell
$ cd tests
$ ansible-playbook kafka.yml

```

## Reference

- https://github.com/aliattari52/Kafka