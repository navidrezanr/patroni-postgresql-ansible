# High Availability PostgreSQL Cluster with Patroni, etcd & Ansible

This repository provides an automated way to deploy a **high-availability PostgreSQL cluster** using **Patroni**, **etcd**, and **Ansible**.

## 🧩 Architecture Overview

- **Ansible Control Node**: Ubuntu server managing the deployment.  
- **etcd Cluster**: Key-value store for Patroni state and leader election.  
- **PostgreSQL Nodes**: Managed by Patroni for replication and automatic failover.  
- **Optional Load Balancer**: HAProxy or Nginx for routing traffic to the current leader node.  


---

## ⚙️ Prerequisites

- Ubuntu (tested on **22.04**)  
- Ansible version **≥ 2.15**  
- SSH access from the control node to all target PostgreSQL server nodes  
- Python 3 installed on all target servers  
- Sudo or root privileges on the target servers  

---

## 🚀 Deployment Steps

1. Clone the repository  
   ```bash
   git clone https://github.com/navidrezanr/patroni-postgresql-ansible.git
   cd patroni-postgresql-ansible
