# Zyprova

🌐 [zyprova.com](https://www.zyprova.com/) | 💼 [LinkedIn](https://www.linkedin.com/company/zyprova/)

> AI Powered Financial Planning & Analysis

---

![](https://img.shields.io/badge/Financial_Planning_%26_Analysis-0A66C2?style=flat) ![](https://img.shields.io/badge/Corporate_Performance_Management-0A66C2?style=flat) ![](https://img.shields.io/badge/FinTech-0A66C2?style=flat) ![](https://img.shields.io/badge/B2B_SaaS-0A66C2?style=flat) ![](https://img.shields.io/badge/Workforce_Planning-0A66C2?style=flat) ![](https://img.shields.io/badge/Equity_%26_Cap_Table_Management-0A66C2?style=flat) ![](https://img.shields.io/badge/Strategic_Planning_%26_Forecasting-0A66C2?style=flat) ![](https://img.shields.io/badge/Business_Intelligence-0A66C2?style=flat) ![](https://img.shields.io/badge/Enterprise_SaaS-0A66C2?style=flat)

---

![](https://img.shields.io/badge/NestJS-E0234E?style=flat&logo=nestjs&logoColor=white) ![](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white) ![](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white) ![](https://img.shields.io/badge/Kafka-231F20?style=flat&logo=apachekafka&logoColor=white) ![](https://img.shields.io/badge/REST_APIs-009688?style=flat) ![](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white) ![](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white) ![](https://img.shields.io/badge/ChromaDB-FF6719?style=flat) ![](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) ![](https://img.shields.io/badge/VueJS-4FC08D?style=flat&logo=vuedotjs&logoColor=white) ![](https://img.shields.io/badge/Microservices_Architecture-6B7280?style=flat)

---

## Table of Contents

1. [Product Overview](#product-overview)
2. [System Architecture](#system-architecture)
3. [Tech Stack](#tech-stack)
4. [Engineering Contributions](#engineering-contributions)

---

## Product Overview

Zyprova is an AI-based corporate planning and forecasting platform that replaces spreadsheets and disconnected planning tools. It lets executives and operators run financial, headcount, and equity planning through natural language instead of formulas.

1. **Conversational Planning:** Ask questions in plain English to generate forecasts, projections, and insights. No spreadsheet formulas or manual modeling required.
1. **Financial Forecasting & Scenario Modeling:** Build and compare best, base, and worst-case projections. Instantly see impact on runway, revenue, burn, and cash flow.
1. **Headcount & Compensation Planning:** Model hiring plans and team growth. Forecast total compensation (salary, bonuses, equity) and adjust assumptions to see cost impact in real time.
1. **Cap Table & Equity Integration:** Map dilution into hiring and fundraising plans. Align equity strategy with financial projections.
1. **Unified Cross-Functional Planning:** One platform for Finance, HR, and operations, with shared access, version control, comments, and permissions.
1. **Board & Investor Reporting:** Generate dashboards and investor-ready reports. Export financial, HR, and equity views instantly.

---

## System Architecture

Zyprova is an event-driven microservices platform built on NestJS, TypeScript, and PostgreSQL, featuring AI-powered integrations through a proprietary LLM and RAG-enabled Slack interface.

### Architecture Diagram

```mermaid
graph TB
    subgraph "Frontend"
        UI[zyprova-ui<br/>Vue.js]
    end

    subgraph "API Layer"
        GW[api-gw<br/>API Gateway<br/>Kafka Producer/Consumer]
    end

    subgraph "Microservices"
        FP[fp-a-ms<br/>Financial Planning]
        HR[hr-ms<br/>Human Resources]
        USER[user-ms<br/>User Accounts]
        SLACK[slack-ms<br/>Slack Integration<br/>LangChain + ChromaDB]
    end

    subgraph "AI Services"
        AI[ai-ms<br/>Proprietary LLM]
    end

    subgraph "Message Queue"
        KAFKA[Kafka Cluster]
    end

    subgraph "Database"
        DB[(PostgreSQL)]
    end

    subgraph "Infrastructure"
        DEPLOY[deployment-tools<br/>Docker Images<br/>AWS Deployment]
        LIB[common-lib<br/>Shared Types/Utils]
    end

    UI --> GW
    GW <--> KAFKA

    KAFKA <--> FP
    KAFKA <--> HR
    KAFKA <--> USER
    KAFKA <--> SLACK

    FP --> DB
    HR --> DB
    USER --> DB
    SLACK --> DB

    SLACK <--> AI

    FP -.- LIB
    HR -.- LIB
    USER -.- LIB
    SLACK -.- LIB
    GW -.- LIB
    AI -.- LIB

    DEPLOY -.-> FP
    DEPLOY -.-> HR
    DEPLOY -.-> USER
    DEPLOY -.-> SLACK
    DEPLOY -.-> GW
    DEPLOY -.-> AI

    style UI fill:#e1f5ff
    style GW fill:#fff4e1
    style KAFKA fill:#ffe1e1
    style DB fill:#e1ffe1
    style AI fill:#f5e1ff
    style LIB fill:#f0f0f0
    style DEPLOY fill:#f0f0f0
```

### Architecture Layers

#### Frontend

**zyprova-ui** is a Vue.js SPA served via CloudFront and S3. It communicates with the backend through the API Gateway.

#### API Layer

**api-gw** is the central gateway routing all microservice communications via Kafka. It implements event-driven patterns for asynchronous processing and handles request validation and routing.

#### Microservices

Each business domain is implemented through an independently deployable microservice with its isolated DB, e.g.:

| Service   | Responsibilities                                          |
| --------- | --------------------------------------------------------- |
| `fp-a-ms` | Financial planning and analysis workflows                 |
| `hr-ms`   | Employee data and HR processes                            |
| `user-ms` | User Accounts, authentication and user profile management |
| `others`  | ...                                                       |

#### AI Services

**slack-ms** is the service that acts as middleware between the company Slack workspace and `ai-ms`, implements the full RAG pattern using LangChain + ChromaDB, stores conversation history for contextual responses, and publishes significant events to Kafka.

**ai-ms** is a wrapper for the proprietary LLM. Isolating it as its own service allows model updates without affecting other services.

#### Infrastructure

**common-lib** provides shared TypeScript types, interfaces, and utilities to reduce code duplication and ensure consistency across services.

**deployment-tools** is a centralized repository for Docker images and AWS deployment automation (infrastructure-as-code and container management).

### RAG Flow (Slack Integration)

```mermaid
sequenceDiagram
    participant User as Slack User
    participant Slack as Company Slack
    participant SlackMS as slack-ms<br/>(LangChain Pipeline)
    participant Chroma as ChromaDB
    participant Kafka as Kafka Queue
    participant AIMS as ai-ms<br/>(Proprietary LLM)
    participant DB as PostgreSQL

    User->>Slack: Send message/query
    Slack->>SlackMS: Webhook/Event

    SlackMS->>DB: Fetch user context
    DB-->>SlackMS: User data

    SlackMS->>Chroma: Vector search<br/>(retrieve context)
    Chroma-->>SlackMS: Relevant documents

    SlackMS->>SlackMS: LangChain pipeline<br/>(prompt engineering)

    SlackMS->>AIMS: Inference request<br/>(context + query)
    AIMS->>AIMS: LLM processing
    AIMS-->>SlackMS: AI response

    SlackMS->>Chroma: Store interaction<br/>(for future context)
    SlackMS->>DB: Log interaction

    SlackMS->>Kafka: Publish event<br/>(if needed)

    SlackMS->>Slack: Format response
    Slack->>User: Display response

    Note over SlackMS,Chroma: ChromaDB acts as<br/>vector memory store<br/>for RAG pattern
```

### AWS Deployment

```mermaid
graph TB
    subgraph "AWS Cloud"
        subgraph "deployment-tools Repository"
            DOCKER[Docker Images<br/>- api-gw<br/>- fp-a-ms<br/>- hr-ms<br/>- slack-ms<br/>- user-ms<br/>- ai-ms]
            IaC[Infrastructure as Code<br/>Deployment Scripts]
        end

        subgraph "Compute Layer"
            direction LR
            GW_CONTAINER[api-gw<br/>Container]
            FP_CONTAINER[fp-a-ms<br/>Container]
            HR_CONTAINER[hr-ms<br/>Container]
            SLACK_CONTAINER[slack-ms<br/>Container]
            USER_CONTAINER[user-ms<br/>Container]
            AI_CONTAINER[ai-ms<br/>Container]
        end

        subgraph "Data Layer"
            RDS[(RDS PostgreSQL<br/>Multi-AZ)]
            KAFKA_CLUSTER[MSK<br/>Managed Kafka Cluster]
            CHROMA_VOL[EBS Volume<br/>ChromaDB Data]
        end

        subgraph "Frontend Hosting"
            S3[S3 Bucket<br/>zyprova-ui]
            CF[CloudFront CDN]
        end

        LB[Application Load Balancer]

        DOCKER -.->|Build & Push| GW_CONTAINER
        DOCKER -.->|Build & Push| FP_CONTAINER
        DOCKER -.->|Build & Push| HR_CONTAINER
        DOCKER -.->|Build & Push| SLACK_CONTAINER
        DOCKER -.->|Build & Push| USER_CONTAINER
        DOCKER -.->|Build & Push| AI_CONTAINER

        CF --> S3
        CF --> LB

        LB --> GW_CONTAINER

        GW_CONTAINER <--> KAFKA_CLUSTER
        FP_CONTAINER <--> KAFKA_CLUSTER
        HR_CONTAINER <--> KAFKA_CLUSTER
        SLACK_CONTAINER <--> KAFKA_CLUSTER
        USER_CONTAINER <--> KAFKA_CLUSTER

        FP_CONTAINER --> RDS
        HR_CONTAINER --> RDS
        SLACK_CONTAINER --> RDS
        USER_CONTAINER --> RDS

        SLACK_CONTAINER --> CHROMA_VOL
        SLACK_CONTAINER <--> AI_CONTAINER
    end

    EXTERNAL[External Users] --> CF
    SLACK_EXT[Slack Workspace] <--> SLACK_CONTAINER

    style DOCKER fill:#f0f0f0
    style IaC fill:#f0f0f0
    style RDS fill:#e1ffe1
    style KAFKA_CLUSTER fill:#ffe1e1
    style CF fill:#e1f5ff
    style S3 fill:#e1f5ff
```

All services are containerized via the `deployment-tools` repository. AWS infrastructure includes an Application Load Balancer for traffic distribution, ECS/EKS for container orchestration, RDS Multi-AZ for high availability, MSK for managed Kafka, and CloudFront + S3 for global frontend delivery.

### Key Architectural Patterns

**Event-Driven Communication:** Kafka enables loose coupling between services. Services publish domain events that others consume asynchronously.

**RAG Implementation:** `slack-ms` uses ChromaDB to retrieve relevant context before LLM inference, enabling accurate, context-aware responses without retraining the model.

**Gateway Pattern:** `api-gw` provides a single entry point, abstracting microservice complexity from the frontend.

**Shared Library:** `common-lib` ensures consistency across services while maintaining independent deployability.

---

## Tech Stack

| Technology           | Rationale                                                                                                    |
| -------------------- | ------------------------------------------------------------------------------------------------------------ |
| NestJS               | Enterprise-grade TypeScript framework with built-in dependency injection, making microservices maintainable  |
| Kafka                | High-throughput message streaming, crucial for event-driven architecture at scale                            |
| PostgreSQL           | ACID compliance for transactional data across financial and HR domains                                       |
| LangChain + ChromaDB | Modern RAG stack enabling contextual AI responses without model fine-tuning                                  |
| Docker + AWS         | Containerization ensures consistent deployments; AWS managed services (RDS, MSK) reduce operational overhead |

---

## Engineering Contributions

- Integrated local LLM and Slack APIs with backend microservices to deploy a proprietary AI assistant within the company's Slack, contributing to a successful funding round evaluation.
- Built an end-to-end microservices pipeline for AI integration, including data preprocessing workflows, RAG capabilities, concurrent request handling, timeout management, and metadata persistence.
- Designed and implemented event-driven workflows across microservices using Kafka and REST APIs, building complex backend services to deliver core business functionality for a fintech platform.
- Led architecture and system design decisions, including database schema design, for implementing new product features and establishing technical standards for code quality.
- Improved system performance and scalability through database normalization, query optimization, refactoring backend services.
- Collaborated with frontend developers, designers, and stakeholders to translate business requirements into technical deliverables.
