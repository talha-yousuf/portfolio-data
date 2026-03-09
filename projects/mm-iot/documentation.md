# Machine Maintenance

> Comprehensive Asset Management & Rental Platform

---

![](https://img.shields.io/badge/Asset_Management-0A66C2?style=flat) ![](https://img.shields.io/badge/IoT-0A66C2?style=flat) ![](https://img.shields.io/badge/PWA-0A66C2?style=flat) ![](https://img.shields.io/badge/B2B_SaaS-0A66C2?style=flat) ![](https://img.shields.io/badge/Field_Operations-0A66C2?style=flat)

---

![](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) ![](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white) ![](https://img.shields.io/badge/Redux-764ABC?style=flat&logo=redux&logoColor=white) ![](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white) ![](https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=white) ![](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white) ![](https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white) ![](https://img.shields.io/badge/Cypress-69D3A7?style=flat&logo=cypress&logoColor=black) ![](https://img.shields.io/badge/Jest-C21325?style=flat&logo=jest&logoColor=white) ![](https://img.shields.io/badge/Material_UI-007FFF?style=flat&logo=mui&logoColor=white) ![](https://img.shields.io/badge/MQTT-660066?style=flat)

---

## Table of Contents

1. [Product Overview](#product-overview)
2. [System Architecture](#system-architecture)
3. [Tech Stack](#tech-stack)
4. [Engineering Contributions](#engineering-contributions)

---

## Product Overview

Machine Maintenance is a comprehensive workspace PWA for management and rentals of physical assets such as electronics, hardware tools, vehicles, and any other equipment that can be monitored via IoT sensors.

1. **Scheduling & Rentals:** Calendar for scheduling events such as rentals and maintenance across assets.
2. **Collaborative Task Planning:** KanBan board for project management, resource allocation, and internal operations such as task tracking and problem reporting.
3. **Role-Based Access:** Admin panel for customizable user roles (such as, admin, manager, employee), each assignable a different level of authorization.
4. **Live Asset Tracking:** Interactive map for real-time equipment tracking using onboard GPS sensors.
5. **IoT Data & Analytics:** Dashboard for data visualization and analytics from integrated and third-party sensors.

Renting agencies, renters, and freelancers can track their rented or owned assets by location and status. Rental agency staff can collaboratively work on internal operations, and users can have roles inside an agency with admin-controlled authorization levels.

---

## System Architecture

### Architecture Layers

#### Frontend

React PWA built with Redux for state management, Material UI for components, LeafletJS for interactive mapping, and Recharts for data visualization and analytics dashboards.

#### Backend

Django REST API backed by PostgreSQL. MQTT used for real-time IoT sensor data ingestion from onboard GPS and third-party sensors.

#### Infrastructure

Jenkins CI/CD pipelines with Docker for containerized frontend deployments on self-hosted servers.

---

## Tech Stack

| Technology          | Rationale                                                                              |
| ------------------- | -------------------------------------------------------------------------------------- |
| React + Redux       | Component-driven UI with centralized state management for complex real-time data flows |
| LeafletJS           | Interactive mapping for live GPS asset tracking                                        |
| Recharts            | Flexible charting for IoT analytics dashboards                                         |
| Django + PostgreSQL | REST API backend with relational data modeling for assets, roles, and schedules        |
| MQTT                | Lightweight pub/sub protocol for real-time IoT sensor data ingestion                   |
| Jenkins + Docker    | CI/CD pipeline for automated builds and self-hosted deployments                        |
| Cypress + Jest      | E2E and unit test coverage enforcing TDD practices                                     |

---

## Engineering Contributions

- Led frontend development of the asset management PWA from scratch, planning and estimating tasks, implementing features, and transitioning into a frontend team lead role as the team scaled.
- Collaborated with backend developers to design entity relationships and REST APIs, and participated in database normalization efforts.
- Built an interactive map for live equipment tracking using onboard GPS sensors, and developed IoT analytics dashboards integrating data from multiple sensor sources.
- Implemented role-based access control with customizable user authorization levels managed through an admin panel.
- Collaborated with the product team, UI/UX designer, and stakeholders to gather business requirements and translate them into technical features.
- Established and maintained Jenkins CI/CD pipelines with Docker for frontend deployments on self-hosted servers using Bash scripts.
- Wrote comprehensive E2E test suites using Cypress for cross-browser and cross-device validation, alongside unit test coverage using Jest, enforcing TDD best practices.
- Implemented GDPR-compliance features to meet data protection regulatory requirements.
