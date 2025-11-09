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
   git clone https://github.com/navidrezanr/patroni-postgresql-ansible.git
   cd patroni-postgresql-ansible

2.Configure your Ansible inventory
   *Edit inventory/hosts.yml (or whichever inventory file you choose) and list your etcd and PostgreSQL nodes
   *Make sure you define groups such as etcd, postgres, etc

3.Run the playbook
ansible-playbook -i inventory/hosts.yml site.yml

4.Verify cluster health
  *SSH into one of the PostgreSQL nodes
  *Use patronictl or equivalent to check leader/follower status
  *Connect to PostgreSQL via psql and run a test query

🔧 Key Features
  *Automated bootstrapping of an etcd cluster
  *Installation and configuration of PostgreSQL with streaming replication
  *Leader election and failover handled by Patroni
  *Optional load balancing layer for directing traffic to the current master
  *Secure SSH and sudoing configuration via Ansible
  *Idempotent playbooks: safely re-run them when needed

  🛠️ Customization & Extension
  *To add more PostgreSQL replicas: add them to the postgres group in your inventory and re-run the playbook.
  *To switch load balancer type (HAProxy ↔ Nginx): adjust the corresponding role vars.
  *Integrate monitoring tools (e.g., pg_stat_statements, Prometheus exporter, pgwatch2) by creating extra roles and linking them into the playbook.
  
  ✅ Usage Scenarios
  *Production environments requiring high availability for PostgreSQL.
  *Lab environments for DevOps training or database reliability testing.
  *Educational/demo setups on how to structure HA database clusters with Ansible.

   
