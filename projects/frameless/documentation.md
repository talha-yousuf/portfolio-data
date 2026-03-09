# Frameless — NFT Marketplace

> A multi-blockchain NFT marketplace where users can mint, buy, and sell NFTs. Built on ZkSync (L2 Ethereum), offering lower gas fees and faster transactions than mainnet.

---

![](https://img.shields.io/badge/Blockchain-6B7280?style=flat) ![](https://img.shields.io/badge/Web3-6B7280?style=flat) ![](https://img.shields.io/badge/NFT-6B7280?style=flat) ![](https://img.shields.io/badge/DeFi-6B7280?style=flat) ![](https://img.shields.io/badge/Digital_Collectibles-6B7280?style=flat) ![](https://img.shields.io/badge/E--Commerce-6B7280?style=flat)

---

![](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) ![](https://img.shields.io/badge/Redux-764ABC?style=flat&logo=redux&logoColor=white) ![](https://img.shields.io/badge/TailwindCSS-06B6D4?style=flat&logo=tailwindcss&logoColor=white) ![](https://img.shields.io/badge/Formik-172B4D?style=flat) ![](https://img.shields.io/badge/web3--react-F16822?style=flat) ![](https://img.shields.io/badge/Recharts-22B5BF?style=flat) ![](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white) ![](https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white) ![](https://img.shields.io/badge/ZkSync-1E69FF?style=flat) ![](https://img.shields.io/badge/Ethereum-3C3C3D?style=flat&logo=ethereum&logoColor=white)

---

## Table of Contents

1. [Product Overview](#product-overview)
2. [Architecture](#architecture)
3. [Tech Stack](#tech-stack)
4. [Engineering Contributions](#engineering-contributions)

---

## Product Overview

Frameless is a full-featured NFT trading platform built on ZkSync, a Layer 2 Ethereum scaling solution using ZK rollup technology. It allows creators and collectors to mint, list, buy, and sell NFTs with significantly reduced gas fees and faster finality compared to Ethereum mainnet. Users can configure collection parameters, set royalties, and manage their portfolios through a polished, responsive interface.

The platform consists of two applications: a customer-facing marketplace and an internal admin CMS.

1. **Customer-Facing Marketplace:** Covers the full user journey — from connecting a wallet and minting an NFT, to browsing listings, viewing activity logs, and completing purchases. Includes forms for creating items and collections, listing pages, user profiles, and product detail pages.
2. **Blockchain Integration:** Interactions are handled via the web3-react library, which manages wallet connections (e.g. MetaMask) and exposes utilities for signing and submitting transactions — including NFT minting and buy/sell workflows — to the ZkSync network.
3. **Admin CMS:** Gives internal teams visibility into platform activity. Dashboards surface real-time analytics on listing volume and NFT popularity, with separate views for user account management and transaction monitoring. Data visualizations are built with Recharts.

---

## Architecture

The frontend is split into two standalone React SPAs — the marketplace app and the admin CMS — each with its own Redux store and routing. Both apps share a common design system built with TailwindCSS, enforcing visual consistency across the platform.

Blockchain interactions follow an async, wallet-first pattern: the user connects their wallet via web3-react, which provides the signer context used to call smart contract functions (minting, transfers, purchases) against the ZkSync network. Transaction state and error handling are managed client-side.

Both applications are containerized with Docker and hosted on self-hosted Linux servers. CI/CD is handled via Jenkins pipelines that run automated tests and deploy on merge.

---

## Tech Stack

| Technology       | Rationale                                                                              |
| ---------------- | -------------------------------------------------------------------------------------- |
| React + Redux    | Component-driven UI with centralized state management across both SPAs                 |
| TailwindCSS      | Utility-first styling enabling a consistent design system built from scratch           |
| web3-react       | Wallet integration and utilities for interacting with Ethereum-based blockchains       |
| ZkSync           | Layer 2 scaling via ZK rollups — lower gas fees and faster finality than mainnet       |
| Recharts         | Data visualization library for admin analytics dashboards                              |
| Docker + Jenkins | Containerized deployments with automated CI/CD pipelines on self-hosted infrastructure |

---

## Engineering Contributions

- Planned and estimated the full frontend scope of the project as the developer responsible for all client-side delivery.
- Built the design system from scratch — layout, reusable components, and custom styling — ensuring consistent UI/UX across both apps.
- Developed the customer-facing marketplace: item and collection creation forms, listing pages, activity logs, user profiles, product detail pages, and the landing page.
- Integrated blockchain functionality using web3-react: wallet connection, NFT minting on ZkSync/ETH, and transaction workflows for buying and selling.
- Built the admin CMS: dashboards for listing oversight, transaction monitoring, real-time analytics, user account management, and activity tracking.
- Implemented data visualizations for admin dashboards using Recharts.
- Conducted code reviews and carried out QA processes.
