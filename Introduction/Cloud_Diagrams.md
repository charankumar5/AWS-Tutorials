# ☁️ Cloud Computing – Diagram & Architecture Visual Guide

This section visually explains:
- Virtualization
- Cloud Model
- Public vs Private Cloud
- AWS Global Infrastructure
- Basic Cloud Architecture

---

# 🎛️ 1. Virtualization Diagram

## 💡 One Physical Server → Many Virtual Machines

```mermaid
flowchart TB
    A[🖥️ Physical Server] --> B[🧠 Hypervisor]
    B --> C[💻 Virtual Machine 1]
    B --> D[💻 Virtual Machine 2]
    B --> E[💻 Virtual Machine 3]
