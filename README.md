# Kustomize: Zero to Hero 🚀

This project demonstrates how to use **Kustomize** to manage and customize Kubernetes YAML configurations for different environments like **development**, **staging**, and **production** — without duplicating code.

---

## 📚 What is Kustomize?

**Kustomize** is a Kubernetes-native configuration management tool that lets you:

Kustomize helps you change Kubernetes files without editing them directly. Think of it like cooking:
- You have a basic recipe (we call this the base)
- You want to make small changes (we call these overlays)
- You don't need to change the original recipe!

It works directly with `kubectl` — no extra tools required!

---
## Topics
1. [Basics](./01-basics/README.md) - Learn what Kustomize is and how to use it
2. [Patches](./02-patches/README.md) - Make specific changes to your files
3. [ConfigMaps and Secrets](./03-configmaps-secrets/README.md) - Work with configuration files
4. [Generators](./04-generators/README.md) - Create configs automatically
5. [Real World Examples](./05-real-world/README.md) - See how to use Kustomize in real projects

## 🧱 Project Structure

```
.
├── base/
│ ├── deployment.yaml
│ ├── service.yaml
│ ├── increase-replicas.yaml
│ └── kustomization.yaml
└── overlay/              # Your customizations
    └── kustomization.yaml # Defines how to modify the base
```

## Understanding the Files

### Base Configuration
The `base/` directory contains your original, unchanged configuration:
- `deployment.yaml`: A simple nginx web server deployment
- `kustomization.yaml`: Lists which files to include

### Overlay Configuration
The `overlay/` directory shows how to customize the base:
- Adds a prefix to all resources (`dev-`)
- Updates the nginx image version to 1.20
- Adds environment labels

## Try It Yourself


### 🔹 base/
Contains the default (common) Kubernetes manifests — shared by all environments.

### 🔹 overlays/development/
Contains environment-specific customizations (for development in this case).

---

## ⚙️ Prerequisites

Before running this project, make sure you have:

- ✅ [kubectl](https://kubernetes.io/docs/tasks/tools/) installed
- ✅ Access to a Kubernetes cluster (like Minikube, OKE, EKS, etc.)

> Kustomize is built-in with `kubectl` (v1.14+)

---

## 🧪 How to Run and Test

### ▶️ 1. See the Base Manifest Output

```bash
kubectl kustomize ./base
```

1. View the base deployment:
```bash
kubectl kustomize base/
```

2. View the customized version:
```bash
kubectl kustomize overlay/
```

3. Apply to your cluster:
```bash
kubectl apply -k overlay/
```

## What's Happening?
1. Kustomize reads the base configuration
2. It applies the changes specified in the overlay:
   - Adds "dev-" prefix to names
   - Updates the nginx image
   - Adds environment labels
3. Generates the final configuration

## Key Concepts
- **Base**: Your original configuration
- **Overlay**: Your customizations
- **kustomization.yaml**: Tells Kustomize what to do
- **Resources**: The Kubernetes files you want to modify
