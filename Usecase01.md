
flowchart LR

%% ===== CLIENT & EDGE =====
User[Web / Mobile Users]
CDN[CDN / Edge]
DNS[DNS]
WAF[DDoS + WAF]

User --> DNS --> CDN --> WAF

%% ===== TRAFFIC & API =====
LB[Load Balancer]
API[API Gateway]

WAF --> LB --> API

%% ===== AUTH =====
Auth[User Authentication]
IAM[Identity & Access Mgmt]

API --> Auth --> IAM

%% ===== COMPUTE LAYER =====
subgraph Compute
  VM[VM Compute]
  AS[Auto Scaling]
  SL[Serverless Functions]
  K8S[Kubernetes Cluster]
end

API --> VM
API --> SL
API --> K8S
VM --> AS

%% ===== CONTAINER SUPPORT =====
CR[Container Registry]
CR --> K8S

%% ===== DATA LAYER =====
subgraph Data
  RDB[Relational Database]
  NoSQL[NoSQL Database]
  Cache[In-Memory Cache]
  Obj[Object Storage]
  File[File Storage]
end

VM --> RDB
VM --> NoSQL
VM --> Cache
VM --> Obj
VM --> File

K8S --> RDB
K8S --> NoSQL
K8S --> Cache

%% ===== ASYNC & EVENTS =====
subgraph Async
  MQ[Message Queue]
  EB[Event Bus]
  Stream[Streaming Platform]
end

API --> MQ
API --> EB
EB --> Stream

%% ===== WORKFLOWS =====
WF[Workflow Orchestration]
MQ --> WF

%% ===== ANALYTICS =====
subgraph Analytics
  DW[Data Warehouse]
  ETL[ETL / Data Integration]
end

Obj --> ETL --> DW
Stream --> DW

%% ===== AI / ML =====
ML[ML Platform]
DW --> ML
ML --> API

%% ===== OBSERVABILITY =====
subgraph Observability
  Mon[Monitoring]
  Logs[Logging]
  Audit[Audit & Compliance]
end

VM --> Mon
K8S --> Logs
API --> Audit

%% ===== SECURITY & CONFIG =====
Secrets[Secrets Manager]
Config[Config / Parameter Store]

Secrets --> VM
Config --> VM

%% ===== DEVOPS =====
subgraph DevOps
  CICD[CI/CD Pipeline]
  IaC[Infrastructure as Code]
end

CICD --> CR
IaC --> Compute
IaC --> Data

%% ===== BACKUP & DR =====
Backup[Backup & DR]
RDB --> Backup
Obj --> Backup

%% ===== HYBRID / EDGE =====
Edge[Hybrid / Edge Infrastructure]
Edge --> CDN