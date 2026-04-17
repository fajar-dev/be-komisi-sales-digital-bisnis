# 🚀 Komisi Sales

[![Bun](https://img.shields.io/badge/Bun-%23000000.svg?style=for-the-badge&logo=bun&logoColor=white)](https://bun.sh)
[![Hono](https://img.shields.io/badge/Hono-%23E36002.svg?style=for-the-badge&logo=hono&logoColor=white)](https://hono.dev)
[![MySQL](https://img.shields.io/badge/mysql-%2300f.svg?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)

Sistem pengelolaan komisi sales yang terintegrasi dengan data invoice dan struktur organisasi perusahaan. Aplikasi ini menangani kalkulasi komisi otomatis, penyesuaian (adjustments), dan penarikan data (crawling) dari sistem utama.

---

## 🛠️ Tech Stack

- **Runtime:** [Bun](https://bun.sh)
- **Framework:** [Hono](https://hono.dev)
- **Database:** MySQL (using `mysql2`)
- **Validation:** [Zod](https://zod.dev)
- **Authentication:** Google OAuth 2.0 & JWT
- **HTTP Client:** Axios
- **Date Utilities:** date-fns

---

## 📁 Project Structure

```text
├── src
│   ├── config        # Database and app configurations
│   ├── controller    # Request handlers (Business Logic)
│   ├── crawl         # Data synchronizer scripts
│   ├── helper        # Shared utility functions (Commission calculations, Periods)
│   ├── middleware    # Authentication & Hierarchy authorization
│   ├── routes        # API Route definitions
│   ├── service       # Data access layer (Database queries)
│   └── main.ts       # Application entry point
├── table.sql         # Database schema
└── package.json      # Dependencies and scripts
```

---

## ⚡ Quick Start

### 1. Prerequisites

Ensure you have **Bun** installed on your machine.

### 2. Installation

```sh
bun install
```

### 3. Environment Setup

Copy `.env.dist` to `.env` and fill in the required credentials.

```sh
cp .env.dist .env
```

### 4. Database Setup

Import the schema from `table.sql` into your MySQL database.

### 5. Running the Application

**Development Mode (Hot Reload):**

```sh
bun run dev
```

**Production Mode:**

```sh
bun run start
```

---

## 🕷️ Crawler System

The system includes a built-in crawler to fetch the latest invoice and employee data.

**Run Crawl:**

```sh
bun run crawl
```

**Crawler Functions:**

- `crawlInternalInvoice()`: Fetches and calculates commissions for internal services.
- `crawlResellInvoice()`: Fetches and calculates commissions for resell products.
- `crawlEmployee()`: Synchronizes employee data and hierarchy.

---

## 📊 Commission Logic Overview

### 🔹 Internal Invoices

- **New Subscription/Upgrade:** 12% - 20% commission depending on service type and contract.
- **Cross-Sell Bonus:** Boosts commission to 15% for certain conditions.
- **Recurring:** 1% commission for invoices after the initial contract period.
- **Special Rule:** For subscriptions > 12 months, the first 12 months receive full commission, and the remainder is treated as recurring.

### 🔹 Resell Invoices

- **New/Upgrade:** 2.5% starting commission.
- **Recurring:** 0.5% commission.

### 🔹 Roles

- **Sales:** Earns direct commission from their assigned customers.
- **Implementator:** Earns commission based on successful implementations and customer retention.
- **Manager:** Earns an override commission (25%) based on the performance of their team.

---

## 🛡️ API Endpoints

### Auth

- `POST /api/auth/google`: Login with Google Account.
- `GET /api/auth/me`: Get current logged-in user details.

### Commissions

- `GET /api/sales/:id/commission`: Yearly commission chart for sales.
- `GET /api/manager/:id/commission`: Team commission summary for managers.
- `GET /api/implementator/:id/commission`: Commission details for implementators.

### Adjustments

- `POST /api/adjustment`: Propose a commission adjustment.
- `POST /api/adjustment/:id/accept`: Approve an adjustment.
- `POST /api/adjustment/:id/decline`: Reject an adjustment.

---

## 📝 License

Copyright © 2024 Nusanet. All rights reserved.
