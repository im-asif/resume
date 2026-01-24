### CI/CD Pipeline Architecture

```mermaid
flowchart LR
    subgraph Developer_Zone
        Dev[Developer] -->|Push Code| Git[GitHub Repo]
    end

    subgraph CI_Process [Continuous Integration - Jenkins]
        Git -->|Webhook| Jenkins
        Jenkins -->|Build| Docker[Docker Build]
        Docker -->|Test| Test[Unit Tests]
        Test -->|Push Image| Registry[(AWS ECR)]
    end

    subgraph CD_Process [GitOps - ArgoCD]
        ArgoCD -->|Watch| Registry
        ArgoCD -->|Sync Changes| K8s
    end

    subgraph Production [AWS EKS Cluster]
        K8s[Kubernetes Namespace] -->|Rolling Update| Pods
    end

    classDef tools fill:#f9f,stroke:#333,stroke-width:2px;
    class Jenkins,Docker,ArgoCD,Registry tools;