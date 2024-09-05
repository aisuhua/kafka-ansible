# kafka-ansible

使用 ansible 快速搭建 kafka 集群。

## 安装

```sh
git clone git@github.com:aisuhua/kafka-ansible.git
cd kafka-ansible

# 按需修改 inventory 、安装目录、用户等信息
vim hosts.ini

ansible-playbook playbook.yaml
```

## 卸载

```sh
ansible-playbook remove.yaml
```

## 特点

- 支持在单机上安装多个不同版本的集群
- 卸载简单，方便来回测试
- 支持开启用户身份认证，只支持 SASL_PLAINTEXT
- 定制简单，该 role 保持了简单

## 兼容性

该脚本在 RHEL7、Kylin V10 SP1/SP2 测试过

## 测试

```sh
# 查看 borker 信息
$ /opt/kafka/3.8.0/server1-kafka1/bin/kafka-broker-api-versions.sh \
  --bootstrap-server 172.31.96.151:19093 \
  --command-config /opt/kafka/3.8.0/server1-kafka1/config/kraft/admin.conf | grep rack
172.31.96.151:19093 (id: 1 rack: null) -> (
172.31.96.151:19095 (id: 3 rack: null) -> (
172.31.96.151:19094 (id: 2 rack: null) -> (
```

## 参考项目

- https://github.com/inomera/kafka-3-cluster 采用 Kraft 并放弃 ZooKeeper
- https://github.com/OT-OSM/redis-setup 参考 tasks 设计

## 参考文章

- [User authentication and authorization in Apache Kafka](https://developer.ibm.com/tutorials/kafka-authn-authz/) Basic Auth 原理
- https://kafka.apache.org/31/generated/kafka_config.html Kafka 配置项含义
- [Install Kafka Cluster(Kraft) with SASL_PLAINTEXT and ACL configs](https://medium.com/@azsecured/install-kafka-cluster-kraft-with-sasl-plaintext-and-acl-configs-ae01a1e0040d) 参考 systemd service、用户认证
- [Authentication using SASL/PLAIN](https://kafka.apache.org/documentation/#security_sasl_plain_brokerconfig) Basic Auth 配置
- [SASL configuration](https://kafka.apache.org/documentation/#security_sasl_brokerconfig)
- [7.5 Authorization and ACLs](https://kafka.apache.org/documentation/#security_authz)
- [基于KRaft模式的kafka集群搭建](https://wiki.sqlfans.cn/linux/kafka-cluster-setup.html) 快速搭建一套基于 Kraft 集群

## TODO

- 安装 kafka-ui
- kafka cluster health check
- create/update/delete topic
- 升级 kafka
