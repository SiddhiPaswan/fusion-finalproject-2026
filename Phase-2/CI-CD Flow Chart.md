## CI/CD Flow Overview

This section illustrates the end-to-end Continuous Integration and Continuous Deployment (CI/CD) flow implemented using Jenkins.

The flow shows how a code change made by a developer is automatically picked up by Jenkins, built, containerized, and deployed to a Kubernetes cluster without any manual intervention. Each stage in the pipeline is executed sequentially to ensure code quality, version control, and reliable application deployment.

By separating the pipeline into **CI** and **CD** phases, the workflow ensures that only successfully built and tested applications are deployed to the Kubernetes environment. This approach improves deployment speed, consistency, and overall system reliability.


#### CI/CD Flow Chart

```
## CI/CD Pipeline vs Real-Life Analogy (Side-by-Side Flow)

| **CI/CD Pipeline Flow** | **Real-Life Example (Food Delivery Analogy)** |
|-------------------------|-----------------------------------------------|
| ```text                 | ```text                                       |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Developer Commit    │ | │ Chef Updates Recipe      │                  |
| │ (GitHub Repo)       │ | │ (New Dish Idea)          │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Git Checkout (CI)   │ | │ Kitchen Gets Recipe      │                  |
| │ Jenkins pulls code  │ | │ (Instructions Collected) │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Maven Build (CI)    │ | │ Prepare Ingredients      │                  |
| │ Compile & Package   │ | │ Measure & Clean Items    │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Docker Build (CI)   │ | │ Cook & Pack Food         │                  |
| │ Create Docker Image │ | │ Ready for Delivery       │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Docker Push (CD)    │ | │ Store in Delivery Hub    │                  |
| │ Push Image to Repo  │ | │ (Central Warehouse)      │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Update K8s YAML     │ | │ Update Delivery Details  │                  |
| │ Update Image Tag    │ | │ Address & Order Version  │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ Deploy to K8s (CD)  │ | │ Deliver to Customer      │                  |
| │ Apply & Rollout     │ | │ Using Delivery Agent     │                  |
| └─────────┬───────────┘ | └────────────┬─────────────┘                  |
|           │             |              │                                |
|           ▼             |              ▼                                |
| ┌─────────────────────┐ | ┌──────────────────────────┐                  |
| │ App Running on K8s  │ | │ Customer Enjoys Meal     │                  |
| │ Live & Accessible   │ | │ Order Successfully Done  │                  |
| └─────────────────────┘ | └──────────────────────────┘                  |
|                     |                                           |

```
### CI/CD Flow Summary

#### **Continuous Integration (CI)**
- **Git Checkout**
- **Maven Build**
- **Docker Build**

#### **Continuous Deployment (CD)**
- **Docker Push**
- **Update Kubernetes Deployment**
- **Deploy to Kubernetes**

This Jenkins pipeline provides a **fully automated, scalable, and reliable CI/CD solution** for deploying applications on Kubernetes.
