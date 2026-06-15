<div align="center">

# Babatunde Yusuf Folorunsho

### Software Engineer · Data Architect · Full-Stack Developer

I design **data models first**, then build the APIs and products on top — across healthcare, cultural platforms, and multi-tenant SaaS.

[![Portfolio](https://img.shields.io/badge/Portfolio-follyb.vercel.app-0ea5e9?style=for-the-badge&logo=vercel&logoColor=white)](https://follyb.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/babatunde-yusuf-folorunsho-390869215)
[![Email](https://img.shields.io/badge/Email-Reach%20Out-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:babatundeyusuffolorunsho@gmail.com)

**Lagos, Nigeria** · Open to remote & hybrid roles

</div>

---

## About Me

I build production software end to end — but I start with the **data layer**. Clear entities, relationships, constraints, and migration paths are what make systems reliable as they scale.

My stack: **Next.js & React** on the frontend, **Node.js, .NET, and FastAPI** on the backend, and **PostgreSQL-first** persistence with **Prisma** and **Entity Framework Core**. I model domains for real products — telemedicine, event platforms, RBAC systems, bookings — not generic CRUD demos.

---

## Data Modeling — What I Do

This is the core of how I work. Every project below starts with a schema that reflects the business domain.

| Modeling focus | How I apply it |
|---|---|
| **Entity–relationship design** | Users, roles, appointments, events, bookings — modeled with correct cardinality and foreign keys |
| **Multi-schema PostgreSQL** | Separate schemas (`public`, `medical`, `user_management`) for domain isolation in healthcare systems |
| **RBAC & multi-tenant identity** | App-scoped roles with composite unique constraints (`userId + roleId + app`) |
| **Enum-driven domains** | `RoleName`, `App`, `UserType`, appointment status — enforced at the database layer |
| **Migration discipline** | SQLite → PostgreSQL upgrades, pooled vs direct URLs, versioned Prisma migrations |
| **Validation at the boundary** | Zod + DTOs aligned with Prisma models so bad data never hits the DB |
| **Seed & fixture strategy** | Reproducible dev/staging data for roles, festivals, admin users, and test patients |

### Example — Multi-app RBAC model

```prisma
enum App { YORUBA_CALENDAR  TAX_FLOW  CLEANING_SERVICE  TICKETING }
enum RoleName { USER  CREATOR  ADMIN  SUPERADMIN  CALENDAR_MANAGER }

model UserRole {
  userId String
  roleId String
  app    App
  @@unique([userId, roleId, app])  // one role per app context
}
```

### Example — Healthcare domain (multi-schema)

```prisma
datasource db {
  provider = "postgresql"
  schemas  = ["medical", "public", "user_management"]
}

model HospitalUser {
  role      String   // STI pattern: Doctor | Patient | LabOfficer
  email     String   @unique
  appointmentsReceived  Appointment[] @relation("recipient")
  appointmentsRequested Appointment[] @relation("requester")
  messagesSent          Message[]
  @@schema("public")
}
```

### Modeling patterns I use regularly

- **Single-table inheritance (STI)** — `HospitalUser.role` for doctor/patient/lab officer variants
- **Soft status fields** — `status`, `account_status`, `verification_status` with audit timestamps
- **Junction tables** — `UserRole`, ticket assignments, festival–Orisa links
- **Audit columns** — `createdAt`, `updatedAt`, `created_by`, `last_modified_by`
- **Indexed lookups** — email, userId, and foreign keys indexed for query performance

---

## Architecture & Diagramming

I document every data model and system design before writing code — using tools that render directly on GitHub.

| Tool | What I use it for |
|------|-------------------|
| **[draw.io](https://app.diagrams.net)** | ER diagrams, C4 architecture, deployment & data flow diagrams |
| **[Mermaid](https://mermaid.js.org)** | ER/sequence/flow charts embedded in GitHub READMEs (no export needed) |
| **[dbdiagram.io (DBML)](https://dbdiagram.io)** | Shareable database schema docs with export to PNG |
| **[PlantUML](https://plantuml.com)** | Sequence diagrams & component diagrams |
| **Prisma Studio / ERD** | Live schema inspection & auto-generated entity graphs |

### Sample diagram repo — host on GitHub

**[data-architecture-diagrams](https://github.com/Follyb2810/follyb2810/tree/main/data-architecture-diagrams)** — sample project with `.drawio`, Mermaid, DBML, and PlantUML files for Platform API, Video Call API, Yoruba Calendar, and PCSS.

```mermaid
erDiagram
    User ||--o{ UserRole : has
    Role ||--o{ UserRole : assigned
    User ||--o{ UserAppProfile : owns
    User {
        string id PK
        string email UK
        enum app
    }
```

> Open `.drawio` files in [diagrams.net](https://app.diagrams.net) → export SVG → embed in any README.

---

## Featured Projects

### [Data Architecture Diagrams](https://github.com/Follyb2810/follyb2810/tree/main/data-architecture-diagrams)
Portfolio repo of ER diagrams, system architecture, and data flows — **draw.io**, **Mermaid**, **DBML**, **PlantUML** — mapped to real projects.

**Includes:** Platform API RBAC · Video Call telemedicine · Yoruba Calendar · PCSS content model

`draw.io` · `Mermaid` · `DBML` · `PlantUML` · `GitHub-hosted`

---

### [DigiDokita Video Call & Chat API](https://github.com/DigiDokita/digi_consultation)
Real-time telemedicine backend — video sessions, live chat, appointment scheduling, and notifications for doctors and patients.

**Data modeling:** Multi-schema PostgreSQL (`medical`, `public`, `user_management`), STI user hierarchy, appointment/message relations, activity logs.

`Node.js` · `TypeScript` · `PostgreSQL` · `Prisma` · `Socket.io` · `Redis` · `RabbitMQ` · `WebRTC` · `JWT`

---

### [Platform API v2 — Multi-Tenant Backend](https://github.com/Follyb2810/platform_api_v2)
Shared backend powering multiple products with unified identity and app-scoped authorization.

**Data modeling:** Central `User` + `Role` + `UserRole` with `App` enum; per-app profiles via `UserAppProfile`; festival/Orisa/ticket domain entities.

`Node.js` · `TypeScript` · `PostgreSQL` · `Prisma` · `Clean Architecture`

---

### [Kọ́jọ́dá — Yoruba Calendar Platform](https://github.com/Follyb2810/yoruba_calendar)
Community platform for Yoruba festivals, Orisa references, event ticketing, and cultural content management.

**Data modeling:** Orisa → Festival relations, role-based event publishing, order/ticket entities, OAuth-linked user accounts.

`Next.js 16` · `PostgreSQL` · `Prisma 7` · `NextAuth` · `Paystack`

---

### [Proficients Cares (PCSS)](https://github.com/Follyb2810/pcs)
Full-stack nonprofit site with inquiries, events, gallery, testimonials, and admin CMS.

**Data modeling:** Normalized content models (`Event`, `Inquiry`, `GalleryItem`, `Testimonial`, `SiteSettings`) with status workflows.

`Next.js 16` · `PostgreSQL` · `Prisma` · `TanStack Query` · `Docker`

---

### [DigiDokita — Healthcare Ecosystem](https://github.com/DigiDokita)
Broader telemedicine work — patient–doctor mobile apps, AI-assisted nursing, and clinical data flows.

**Data modeling:** Patient health records, test results, triage data, notification preferences per user type.

`FastAPI` · `Flutter` · `Prisma` · `scikit-learn` · `PostgreSQL`

---

### [Cleaning Service API](https://github.com/Follyb2810/CleaningServiceAPI)
.NET API for bookings, subscriptions, cleaner assignment, and service lifecycle management.

**Data modeling:** EF Core entities for Customer/Cleaner/Admin roles, booking state machine, subscription plans.

`ASP.NET Core 8` · `Entity Framework Core` · `PostgreSQL` · `JWT`

---

## What I Bring to a Team

| Software Engineering | Data Architecture & Modeling |
|---|---|
| Full-stack apps with Next.js, React, TypeScript | Relational schema design (PostgreSQL, Prisma, EF Core) |
| REST APIs, real-time (Socket.io), admin dashboards | Multi-schema layouts & domain-driven table design |
| Mobile with Flutter & React Native | RBAC models, STI patterns, composite constraints |
| Dockerized deployments & CI-ready workflows | Migration governance, seed strategies, Zod validation |
| Healthcare & marketplace domain experience | SQLite → Postgres upgrade paths & connection pooling |
| Architecture docs with draw.io, Mermaid, DBML | ER diagrams, sequence flows, schema docs on GitHub |

---

## Tech Stack

**Languages**
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![C#](https://img.shields.io/badge/C%23-512BD4?style=flat-square&logo=csharp&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

**Frontend**
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Flutter](https://img.shields.io/badge/Flutter-02569B?style=flat-square&logo=flutter&logoColor=white)

**Backend & Data**
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-512BD4?style=flat-square&logo=dotnet&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)

**Architecture & Diagramming**
![draw.io](https://img.shields.io/badge/draw.io-Diagrams-FF6B35?style=flat-square&logo=diagramsdotnet&logoColor=white)
![Mermaid](https://img.shields.io/badge/Mermaid-Diagrams-FF3670?style=flat-square&logo=mermaid&logoColor=white)
![PlantUML](https://img.shields.io/badge/PlantUML-Diagrams-000000?style=flat-square)
![DBML](https://img.shields.io/badge/DBML-dbdiagram.io-00618A?style=flat-square)

---

## GitHub Activity

<div align="center">

[![GitHub Stats](https://github-readme-stats.vercel.app/api?username=Follyb2810&show_icons=true&theme=tokyonight&hide_border=true&count_private=true)](https://github.com/Follyb2810)
[![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=Follyb2810&layout=compact&theme=tokyonight&hide_border=true)](https://github.com/Follyb2810)

</div>

---

## Currently Learning & Exploring

- PostgreSQL indexing, query plans, and performance tuning
- Event-driven architecture for multi-tenant data platforms
- ML feature pipelines integrated with clinical data models

---

## Let's Connect

Open to **Software Engineer**, **Data Architect**, and **Full-Stack Developer** roles — especially where schema design, API platforms, or healthcare/cultural tech matter.

[![GitHub](https://img.shields.io/badge/GitHub-Follyb2810-181717?style=for-the-badge&logo=github)](https://github.com/Follyb2810)
[![Portfolio](https://img.shields.io/badge/Website-follyb.vercel.app-000000?style=for-the-badge&logo=safari&logoColor=white)](https://follyb.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/babatunde-yusuf-folorunsho-390869215)
[![Twitter](https://img.shields.io/badge/Twitter-@babatunde2810-1DA1F2?style=for-the-badge&logo=x&logoColor=white)](https://twitter.com/babatunde2810)
[![Medium](https://img.shields.io/badge/Medium-@follyb2810-12100E?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/@follyb2810)

---

<div align="center">

*"Good software starts with good data models."*

</div>
