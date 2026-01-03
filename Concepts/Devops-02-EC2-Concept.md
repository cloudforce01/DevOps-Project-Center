## Cloud Computing Overview and AWS EC2 Concepts

### Metadata Information

| **Description**                                                            | Est. Read Time | **Keywords**                          | **Author** | **Date**   | **Categories**       | **Tags**                   |
| -------------------------------------------------------------------------- | -------------- | ------------------------------------- | ---------- | ---------- | -------------------- | -------------------------- |
| An overview of cloud computing providers, core AWS EC2 concepts, and FAQs. | 7 - 10 min     | Cloud Computing, AWS, EC2, GCP, Azure | BU         | 2025-12-27 | Cloud Computing, AWS | cloud, EC2, infrastructure |

--------------

👉 Ready for the hands‑on part? The theory is covered below. When you’re comfortable with the concepts, jump straight to the practical lab:

<a href="../Labs/Devops-02-Lab-01-Spin-Up-An-EC2-Instance.md#metadata-information" target="_blank" rel="noreferrer noopener" title="Ctrl/Cmd‑click or Middle‑click to open in a new tab"> ▶️ **Run the Lab** → Devops-02-Lab-01-Spin-Up-An-EC2-Instance - jump to "📊 Metadata Information </a>

----------------

### 📄 Summary

| #                                | Topic                                                     | Core Take‑aways                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1️⃣ Cloud‑Computing Overview** | Major public‑cloud providers and their headline services. | **AWS** – EC2, S3, RDS … <br>**GCP** – Compute Engine, Cloud Storage, BigQuery … <br>**Azure** – Virtual Machines, Blob Storage, Cosmos DB … <br>All give on‑demand compute, storage, networking and managed services for any scale.                                                                                                                                                                                                                                                                                                              |
| **2️⃣ Core AWS EC2 Concepts**    | Vocabulary you’ll meet when working with EC2.             | • **EC2** – virtual servers (instances). <br>• **Region** – geographic data‑center area (~30 worldwide). <br>• **Availability Zone (AZ)** – isolated cluster inside a region for high‑availability. <br>• **Instance / Instance type** – the VM and its CPU/RAM profile (e.g., t2.micro = 1 vCPU + 1 GiB RAM). <br>• **Key pair** – RSA/Ed25519 public‑private keys; private *.pem* stays on your workstation. <br>• **Security group** – virtual firewall controlling inbound/outbound traffic. <br>• **SSH** – encrypted remote‑login protocol. |

### 1️⃣ ☁️ Cloud‑Computing Overview

| ☁️ **Provider** | 🌐 **Primary Offering**                      |
| --------------- | -------------------------------------------- |
| **AWS**         | Elastic Compute Cloud (EC2), S3, RDS, …      |
| **GCP**         | Compute Engine, Cloud Storage, BigQuery, …   |
| **Azure**       | Virtual Machines, Blob Storage, Cosmos DB, … |

These platforms deliver on‑demand compute, storage, networking, and a suite of managed services for enterprises of any size.

---

### 2️⃣ 🔹 Core Concepts of AWS EC2

| 🔹 **Concept**                  | 🗒️ **Description**                                                                                                                        |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **EC2 (Elastic Compute Cloud)** | Service that provisions virtual servers (called *instances*) in the cloud.                                                                 |
| **Region**                      | Physical location of AWS data‑centers (≈ 30 worldwide).                                                                                    |
| **Availability Zone (AZ)**      | Isolated data‑center clusters *within* a region; multiple AZs give high availability.                                                      |
| **Instance**                    | The virtual server you launch.                                                                                                             |
| **Instance type**               | Determines CPU, RAM, storage (e.g., `t2.micro` = 1 vCPU + 1 GiB RAM, burstable).                                                           |
| **Key pair**                    | Public‑/private‑key set (RSA or Ed25519). Private key (`.pem`/`.ppk`) stays on your workstation; public key is injected into the instance. |
| **Security Group**              | Virtual firewall that controls inbound/outbound traffic.                                                                                   |
| **SSH (Secure Shell)**          | Encrypted protocol used to log into the remote Linux host.                                                                                 |

### ❓ Question & Answer

| #      | Question                                                                           | Answer                                                                                                                                                                            |
| ------ | ---------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Q1** | *What are the three biggest public‑cloud providers and one flagship service each?* | **AWS** – Elastic Compute Cloud (EC2); **Google Cloud Platform (GCP)** – Compute Engine; **Microsoft Azure** – Virtual Machines.                                                  |
| **Q2** | *What is an AWS Availability Zone (AZ) and why is it important?*                   | An AZ is an isolated data‑center cluster within a region. Deploying resources across multiple AZs gives fault tolerance; if one AZ fails, the others keep running.                |
| **Q3** | *How does a key pair secure SSH access to an EC2 instance?*                        | The public key is injected into the instance at launch. The private *.pem* key stays on your workstation; SSH uses it to prove identity, allowing password‑less, encrypted login. |
| **Q4** | *Can you launch an Ubuntu EC2 instance without using the AWS Management Console?*  | Yes – you can use the AWS CLI (`aws ec2 run-instances …`) or infrastructure‑as‑code tools (CloudFormation, Terraform). The console steps described are the UI equivalent.         |
| **Q5** | *What is the purpose of a Security Group attached to an EC2 instance?*             | It acts as a virtual firewall that controls inbound and outbound traffic. For SSH you typically allow inbound TCP port 22 from your public IP address.                            |

--------------------

👉 Ready for the hands‑on part? The theory is covered above. When you’re comfortable with the concepts, jump straight to the practical lab: 

<a href="../Labs/Devops-02-Lab-01-Spin-Up-An-EC2-Instance.md#metadata-information" target="_blank" rel="noreferrer noopener"  title="Ctrl/Cmd‑click or Middle‑click to open in a new tab"> ▶️ **Run the Lab** → Devops-02-Lab-01-Spin-Up-An-EC2-Instance - jump to "📊 Metadata Information </a>

----------
