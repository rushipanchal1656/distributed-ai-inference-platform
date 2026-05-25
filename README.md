# 🚀 Distributed AI Inference Platform

A production-style distributed AI inference platform built using AWS, Terraform, Python, TypeScript, and the iii distributed worker framework.

This project demonstrates how modern cloud-native AI systems can distribute inference workloads across multiple nodes using RPC communication, worker meshes, and remote execution patterns.

---

# 🏗️ Architecture Overview


![Architecture Diagram](./architecture-diagram.png)

## 🔥 High-Level Flow

Client Request
⬇
HTTP API Gateway
⬇
TypeScript Caller Worker
⬇
Distributed RPC Call
⬇
Remote Python Inference Worker
⬇
Gemma-3-270m GGUF Model
⬇
Inference Response

---

# ☁️ Cloud Infrastructure

## AWS Services Used

* ✅ AWS EC2
* ✅ VPC
* ✅ Public Subnet
* ✅ Private Subnet
* ✅ Security Groups
* ✅ Internet Gateway
* ✅ NAT-based outbound internet access
* ✅ SSH Bastion-style access
* ✅ Route Tables

---

# 🧠 AI & Backend Technologies

* ✅ Python
* ✅ TypeScript
* ✅ Node.js
* ✅ Transformers
* ✅ Hugging Face GGUF models
* ✅ Gemma-3-270m
* ✅ OpenTelemetry
* ✅ WebSocket-based worker mesh

---

# ⚙️ DevOps & Infrastructure Technologies

* ✅ Terraform
* ✅ tmux
* ✅ Linux
* ✅ SSH
* ✅ Git & GitHub
* ✅ Distributed RPC architecture
* ✅ Infrastructure as Code (IaC)

---

# 🌐 Infrastructure Design

## 📡 API Gateway Node (Public Subnet)

### Responsibilities

* Runs iii Engine
* Exposes HTTP API
* Handles external traffic
* Hosts TypeScript caller-worker
* Routes distributed inference requests

### Components

* iii Engine
* iii-http
* TypeScript Worker
* OpenTelemetry Logging

---

## 🤖 Inference Worker Node (Private Communication)

### Responsibilities

* Runs Python inference worker
* Loads Gemma GGUF model
* Performs AI inference
* Handles distributed RPC requests

### Components

* Python Worker
* Transformers
* GGUF Model
* Remote Worker Registration

---

# 📂 Project Structure

```text
distributed-ai-inference-platform/
│
├── terraform/
│   ├── VPC
│   ├── EC2
│   ├── Security Groups
│   ├── Networking
│   └── Infrastructure Automation
│
├── quickstart/
│   ├── config.yaml
│   └── workers/
│       ├── caller-worker/
│       └── inference-worker/
│
├── screenshots/
├── monitoring/
├── docs/
└── README.md
```

---

# 🔄 Request Flow

## Step-by-Step Flow

1️⃣ Client sends POST request

2️⃣ iii-http receives HTTP request

3️⃣ TypeScript caller-worker receives request

4️⃣ caller-worker invokes:

```ts
inference::run_inference
```

5️⃣ Distributed RPC request is sent to remote Python worker

6️⃣ Python worker loads GGUF model

7️⃣ AI inference executes

8️⃣ Response is returned back through RPC mesh

9️⃣ HTTP response is returned to client

---

# 🔐 Networking & Security

## Security Groups

### API Gateway Security Group

Allowed:

* Port 22 (SSH)
* Port 3111 (HTTP API)
* Port 49134 (iii Worker Communication)

### Private Worker Security Group

Allowed:

* Port 22 (SSH)
* Port 49134 (Worker Mesh Communication)

---

# 🌍 Distributed System Features

## ✅ Multi-node Architecture

Workers communicate across different EC2 instances using private networking.

---

## ✅ RPC-based Communication

Distributed worker-to-worker calls using:

* WebSocket mesh
* iii distributed framework
* Function-based RPC routing

---

## ✅ Multi-language Workers

* TypeScript Worker
* Python Worker

working together in one distributed system.

---

## ✅ Remote AI Execution

Inference workload runs remotely on a dedicated worker node.

---

# 🛠️ Problems Faced & Solutions

## ❌ Terraform State Lock Issues

### Problem

Terraform state lock prevented execution.

### Solution

* Identified stale lock
* Killed hanging Terraform processes
* Cleared corrupted lock state

---

## ❌ SSH Jump/Bastion Connectivity Issues

### Problem

Could not SSH into private worker nodes.

### Solution

* Configured SSH agent forwarding
* Used ProxyJump
* Added proper PEM key handling

---

## ❌ NAT & Internet Access Problems

### Problem

Private worker could not access internet.

### Solution

* Enabled IP forwarding
* Configured NAT routing
* Verified outbound connectivity

---

## ❌ Python Virtual Environment Errors

### Problem

`python3-venv` package missing.

### Solution

Installed:

```bash
sudo apt install python3.12-venv
```

---

## ❌ iii Worker Registration Failures

### Problem

Workers failed to register properly.

### Solution

* Fixed worker paths
* Corrected `config.yaml`
* Re-registered workers

---

## ❌ KVM Runtime Issues

### Problem

iii VM execution failed because KVM unavailable.

### Solution

* Switched to manual worker execution
* Used direct runtime execution approach

---

## ❌ RPC Communication Hanging

### Problem

HTTP requests hung indefinitely.

### Root Cause

Inference worker generated extremely large outputs:

```python
max_new_tokens=32000
```

### Solution

Reduced generation size:

```python
max_new_tokens=128
```

---

## ❌ OOM (Out of Memory) Errors

### Problem

Python inference process killed by Linux OOM Killer.

### Root Cause

Small EC2 instance with large GGUF inference workload.

### Solution

* Optimized inference settings
* Reduced token generation size
* Debugged kernel OOM logs

---

## ❌ tmux Session & Worker Persistence Issues

### Problem

Long-running workers terminated after SSH disconnect.

### Solution

* Used tmux persistent sessions
* Created isolated worker sessions

---

# 📊 Observability & Debugging

## Implemented

* ✅ OpenTelemetry tracing
* ✅ Worker registration logs
* ✅ RPC debugging
* ✅ Distributed request tracing
* ✅ tmux session monitoring

---

# 🧪 Example API Request

```bash
curl -X POST http://<PUBLIC_IP>:3111/v1/chat/completions \
-H "Content-Type: application/json" \
-d '{
  "messages": [
    {
      "role": "user",
      "content": "What is Kubernetes?"
    }
  ]
}'
```

---

# 📚 Key Learnings

## This project helped me learn:

* Distributed system architecture
* AI infrastructure engineering
* Terraform-based provisioning
* RPC communication patterns
* Worker mesh communication
* Multi-node debugging
* Infrastructure troubleshooting
* NAT & VPC networking
* Remote inference execution
* Cloud-native AI design
* OpenTelemetry tracing
* Production debugging workflows

---

# 🚀 Future Improvements

* Kubernetes deployment
* GPU-based inference
* Streaming token responses
* Redis/RabbitMQ integration
* Autoscaling worker pools
* Prometheus & Grafana monitoring
* CI/CD automation
* Dockerized deployment
* High availability architecture

---

# 👨‍💻 Author

## Rushikesh Panchal

### 🔗 GitHub

https://github.com/rushipanchal1656

### 🔗 LinkedIn

https://www.linkedin.com/in/rushikesh-panchal-devops

---

# ⭐ Project Summary

This project demonstrates a real-world distributed AI inference architecture using cloud-native infrastructure, distributed workers, remote execution, RPC communication, and infrastructure automation patterns commonly used in modern AI platforms and production cloud environments.
