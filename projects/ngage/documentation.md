# nGAGE at Work

🌐 [ngageatwork.com](https://ngageatwork.com) | 💼 [LinkedIn](https://www.linkedin.com/company/ngageatwork/) | 📱 [Playstore](https://play.google.com/store/apps/details?id=com.ngageatwork.ngage) | 🍎 [Appstore](https://apps.apple.com/nz/app/n-gage/id1550557086)

> AI-Powered, Gamified Employees Performance Management Platform

---

![](https://img.shields.io/badge/HR_Tech-0A66C2?style=flat) ![](https://img.shields.io/badge/B2B_SaaS-0A66C2?style=flat) ![](https://img.shields.io/badge/Enterprise_Software-0A66C2?style=flat) ![](https://img.shields.io/badge/Mobile--First-0A66C2?style=flat) ![](https://img.shields.io/badge/Employee_Performance_Management-0A66C2?style=flat) ![](https://img.shields.io/badge/Continuous_Feedback-0A66C2?style=flat) ![](https://img.shields.io/badge/Productivity_Tracking-0A66C2?style=flat) ![](https://img.shields.io/badge/Leave_Management-0A66C2?style=flat) ![](https://img.shields.io/badge/Gamification-0A66C2?style=flat) ![](https://img.shields.io/badge/Team_Analytics-0A66C2?style=flat)

---

![](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) ![](https://img.shields.io/badge/NestJS-E0234E?style=flat&logo=nestjs&logoColor=white) ![](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white) ![](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazonaws&logoColor=white)

---

## Table of Contents

1. [Product Overview](#product-overview)
2. [Key Differentiators](#key-differentiators)
3. [System Architecture](#system-architecture)
4. [Engineering Contributions](#engineering-contributions)

---

## Product Overview

nGAGE is an AI-powered, gamified people performance management platform available on iOS, Android, and web. The platform targets mid-to-large organizations looking to manage employee productivity, engagement, and growth without juggling multiple tools.

1. **Growth Gamification:** A points-and-rewards system that ties task completion and challenges directly to employee motivation, with a real reward store employees can spend their points in. Includes leaderboards for individual and team rankings, and a real-time feedback loop tied directly into the rewards flow.
1. **Employee Productivity:** Tracks productive hours, break patterns, and daily pace without invasive monitoring. Includes remote workforce support, leave management (in-app applications and quota tracking), and HRM data export.
1. **Employee Engagement:** Ongoing challenges, sentiment tracking, and leaderboard transparency keep employees invested. Managers can track how organizational changes affect morale over time.
1. **Continuous Feedback:** Replaces annual reviews with structured, ongoing feedback, covering performance category ratings, feedback history, anonymous mode, self-evaluations, proactive feedback requests, and 360 review support.

---

## Key Differentiators

- **AI-Powered Analytics:** Real-time, AI-driven insights surface performance trends and inform decision-making, going beyond raw data to deliver actionable intelligence.
- **MBTI Integration:** Myers-Briggs personality type data is woven into the platform to give managers visibility into team dynamics, individual working styles, and collaboration patterns.
- **Personalized Upskilling:** Learning paths tailored per employee based on role, performance data, and goals, enabling targeted skill development rather than generic company-wide training.

---

## System Architecture

A microservices platform built on NestJS and deployed on AWS, serving both a React web app and a cross-platform mobile app (iOS/Android).

### Architecture Diagram

```mermaid
graph TB
    subgraph "Client"
        WEB[React Web<br/>AWS Hosted]
        MOB[Mobile App<br/>iOS / Android]
    end

    subgraph "Gateway"
        GW[API Gateway<br/>Routing · Auth · Rate Limiting]
    end

    subgraph "Microservices · NestJS · AWS"
        AUTH[Auth Service<br/>JWT · Sessions · Permissions]
        FSVC_A[Feature Svc A<br/>Feedback · Performance]
        FSVC_B[Feature Svc B<br/>Productivity · Attendance]
        FSVC_C[Feature Svc C<br/>Gamification · Engagement]
        NOTIF[Notifications<br/>Real-time · WebSockets]
        ANALYTICS[Analytics<br/>AI · Trends]
    end

    subgraph "Data"
        DB_AUTH[(PostgreSQL<br/>Auth · Users)]
        DB_FEAT[(PostgreSQL<br/>Features · Events)]
        DB_ANALYTICS[(PostgreSQL<br/>Analytics · Logs)]
    end

    WEB <-->|REST, WS| GW
    MOB <-->|REST, WS| GW

    GW --> AUTH
    GW --> FSVC_A
    GW --> FSVC_B
    GW --> FSVC_C

    FSVC_A --> NOTIF
    FSVC_B --> ANALYTICS

    AUTH --> DB_AUTH
    FSVC_A --> DB_FEAT
    FSVC_B --> DB_FEAT
    FSVC_C --> DB_FEAT
    ANALYTICS --> DB_ANALYTICS

    style WEB fill:#141414,stroke:#c8f04c,color:#c8f04c
    style MOB fill:#141414,stroke:#c8f04c,color:#c8f04c
    style GW fill:#161616,stroke:#4cf0a8,color:#4cf0a8
    style AUTH fill:#141414,stroke:#2e2e2e,color:#ccc
    style FSVC_A fill:#141414,stroke:#2e2e2e,color:#ccc
    style FSVC_B fill:#141414,stroke:#2e2e2e,color:#ccc
    style FSVC_C fill:#141414,stroke:#2e2e2e,color:#ccc
    style NOTIF fill:#141414,stroke:#2e2e2e,color:#ccc
    style ANALYTICS fill:#141414,stroke:#2e2e2e,color:#ccc
    style DB_AUTH fill:#0d0d0d,stroke:#222,color:#666
    style DB_FEAT fill:#0d0d0d,stroke:#222,color:#666
    style DB_ANALYTICS fill:#0d0d0d,stroke:#222,color:#666
```

### Architecture Layers

#### Client Layer

A **React web app** (AWS hosted) and a cross-platform **mobile app** (iOS/Android) both connect to the backend, via **REST** for standard operations and **WebSockets** for real-time features like live feedback and notifications.

#### API Gateway

Single entry point in front of all services. Handles **request routing**, auth verification, and rate limiting centrally, so individual services stay focused on their domain logic.

#### Microservices

Each domain runs as an independent **NestJS service on AWS**: Auth, feature services (Feedback/Performance, Productivity/Attendance, Gamification/Engagement), Notifications, and Analytics. Each service is independently deployable and scalable.

#### Data Layer

Each service owns its own **PostgreSQL database**, keeping data concerns isolated by domain. Schemas were designed with **relational integrity** in mind, optimized for read-heavy analytics and leaderboards alongside write-heavy feedback collection.

#### Real-Time

The Notifications service uses **WebSockets** to push live updates to clients, enabling instant feedback alerts, leaderboard updates, and challenge completions without polling.

---

## Engineering Contributions

- Designed and implemented RESTful APIs and NestJS microservices on AWS across several features.
- Built real-time notification pipelines using WebSockets and end-to-end 360-degree evaluation workflows.
- Designed PostgreSQL schemas across multiple service domains, optimized for read-heavy analytics and write-heavy feedback collection.
- Built out full React UI across all major feature areas.
- Owned features end-to-end from database schema through API to rendered UI.
