graph TB
    subgraph "OpenShift/Kubernetes Cluster"
        subgraph "GitLab Namespace"
            GL["GitLab Server"]
            GR["GitLab Registry"]
            GR_DB["GitLab Database"]
        end
        
        subgraph "CI/CD Namespace"
            GR_RUNNER["GitLab Runners"]
            SONAR["SonarQube"]
            NEXUS["Nexus Repository"]
            VAULT["HashiCorp Vault"]
        end
        
        subgraph "Monitoring Namespace"
            PROM["Prometheus"]
            GRAF["Grafana"]
            ELK["ELK Stack"]
            ALERT["AlertManager"]
        end
        
        subgraph "Security Namespace"
            SNYK["Snyk Scanner"]
            AQUA["Aqua Security"]
            FALCO["Falco"]
        end
        
        subgraph "Application Namespaces"
            subgraph "Development"
                PHP_DEV["PHP App"]
                PY_DEV["Python App"]
                JAVA_DEV["Java App"]
            end
            
            subgraph "Staging"
                PHP_STG["PHP App"]
                PY_STG["Python App"]
                JAVA_STG["Java App"]
            end
            
            subgraph "Production"
                PHP_PROD["PHP App"]
                PY_PROD["Python App"]
                JAVA_PROD["Java App"]
            end
        end
    end
    
    subgraph "External Storage"
        NFS["NFS Storage"]
        BACKUP["Backup Storage"]
    end
    
    DEV["Developers"] --> GL
    GL --> GR_RUNNER
    GR_RUNNER --> SONAR
    GR_RUNNER --> NEXUS
    GR_RUNNER --> GR
    PROM --> GRAF
    PROM --> ALERT
    GL --> NFS
    BACKUP --> NFS
