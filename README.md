# Distributed AI Inference Platform

This repository contains infrastructure, scripts, and worker examples for a distributed AI inference platform. This is a skeleton created by the assistant.


# Distributed AI Inference Platform

A production-style distributed AI inference platform built using Terraform, AWS EC2, Python, TypeScript, and iii distributed workers.

This project demonstrates a multi-node architecture where:

* an API Gateway worker receives HTTP inference requests,
* a TypeScript caller-worker routes requests through the iii distributed mesh,
* and a dedicated Python inference-worker performs LLM inference remotely.

The platform was designed to simulate real-world distributed AI infrastructure patterns used in modern cloud-native systems.

---

# Architecture Overview

Client Request
↓
HTTP API Gateway (iii-http)
↓
TypeScript Caller Worker
↓
Distributed RPC Call
↓
Remote Python Inference Worker
↓
Gemma-3-270m GGUF Model
↓
Inference Response

---

# Technologies Used

## Cloud & Infrastructure

* AWS EC2
* Terraform
* VPC
* Public & Private Subnets
* Security Groups
* NAT-based outbound internet routing

## Backend & AI

* Python
* TypeScript
* Node.js
* Transformers
* Hugging Face GGUF models
* Gemma-3-270m

## Distributed Systems

* iii distributed worker framework
* RPC-based worker communication
* OpenTelemetry tracing
* WebSocket worker mesh

## DevOps & Operations

* tmux
* Linux
* SSH Bastion Architecture
* Process orchestration
* Distributed debugging

---

# Infrastructure Design

## API Gateway Node

Responsibilities:

* Runs iii engine
* Exposes HTTP API endpoint
* Hosts TypeScript caller-worker
* Routes inference requests

## Inference Worker Node

Responsibilities:

* Runs Python inference worker
* Loads GGUF language model
* Executes remote inference requests
* Communicates over distributed RPC mesh

---

# Features

* Distributed worker architecture
* Remote AI inference execution
* HTTP-to-RPC request routing
* Multi-language worker interoperability
* OpenTelemetry instrumentation
* Terraform-based provisioning
* Private subnet communication
* Persistent worker execution using tmux

---

# Network Architecture

* Public subnet for API Gateway
* Private subnet communication between workers
* Controlled internet access
* Secure SSH access using bastion pattern

---

# Key Engineering Challenges Solved

## Distributed Worker Communication

Successfully configured remote worker registration across multiple EC2 instances using iii WebSocket communication.

## NAT & Internet Connectivity

Configured outbound internet access for private resources and model downloads.

## Resource Constraints

Handled CPU-only GGUF inference on constrained infrastructure.

## Distributed Debugging

Resolved:

* worker registration conflicts
* stale websocket sessions
* port conflicts
* OOM kills
* RPC routing issues
* SSH session persistence issues

---

# API Endpoint

POST /v1/chat/completions

Example:

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

# Repository Structure

```text
quickstart/
├── workers/
│   ├── caller-worker/
│   │   └── TypeScript API worker
│   └── inference-worker/
│       └── Python LLM inference worker
├── config.yaml
└── iii.worker.yaml
```

---

# Future Improvements

* GPU-backed inference
* Kubernetes deployment
* Streaming token responses
* Autoscaling worker pools
* Redis/RabbitMQ integration
* vLLM/TGI optimization
* Prometheus/Grafana observability
* CI/CD automation

---

# Learning Outcomes

This project provided hands-on experience with:

* distributed systems design
* AI infrastructure engineering
* cloud networking
* remote worker orchestration
* RPC communication patterns
* production debugging methodologies
* infrastructure automation

---

# Author

Rushikesh Panchal

GitHub:
https://github.com/rushipanchal1656

LinkedIn:
https://www.linkedin.com/in/rushikesh-panchal-3869b8241
