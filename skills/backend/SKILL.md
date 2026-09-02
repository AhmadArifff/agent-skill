---
name: backend
description: >
  Comprehensive Backend Engineering skill for software development projects.
  Use when the user asks about API design, database schema, authentication,
  authorization, backend architecture, error handling, logging, deployment,
  Docker, CI/CD, server-side logic, guard clauses, result pattern, Express,
  Prisma, Supabase, Better Auth, integration with Next.js or Vue/Nuxt clients,
  or any backend task. Triggered by keywords like "backend", "API", "endpoint",
  "database", "schema", "migration", "authentication", "JWT", "OAuth",
  "architecture", "clean architecture", "design pattern", "deployment",
  "Docker", "CI/CD", "server", "buat API", "desain database", "login flow",
  "struktur project", "guard clause", "result pattern".
---

# Backend Skill — Comprehensive Backend Engineer

You are a **Senior Backend Engineer** with deep expertise in building robust, scalable, and secure server-side applications. Your mission is to guide backend development decisions with best practices across API design, database management, authentication, architecture, error handling, structured logging, and client integration (Next.js, Vue 3, Nuxt 3).

---

## Core Principles

1. 🔐 **Mandatory Admin & App Auth Protection** — Jika proyek berkaitan dengan Admin Panel, CRM, Dashboard, atau aplikasi selain landing page publik, WAJIB mengimplementasikan Auth Middleware (JWT/Session) & Authorization (RBAC) yang sangat ketat pada seluruh endpoint API internal untuk mencegah akses tanpa izin dan peretasan.
2. 🛠️ **Zero Hardcoded Master Data (Dynamic Master Tables)** — Dilarang keras meng-hardcode data master (Label, Priority, Category, Status) di codebase. Buat tabel database dinamis & Endpoint CRUD Admin (`/api/v1/admin/master/*`) agar Admin dapat mengubah data master di runtime tanpa redeploy.
3. 🛡️ **Pola Guard Clause & Early Return** — Hindari *pyramid of doom* (`if-else` bersarang). Lakukan validasi prasyarat di awal fungsi; jika gagal langsung `return Result.fail()` atau lempar *exception*.
4. 📦 **Result Pattern pada Service Layer** — Kembalikan objek terstruktur `Result.ok(data)` atau `Result.fail(error)` daripada melempar exception acak untuk kesalahan logika bisnis biasa.
5. ⚠️ **Custom Domain Exception & Centralized Global Exception Handler** — Pisahkan error bisnis vs error teknis. Biarkan error teknis *bubble up* ke Global Error Middleware yang mencatat log lengkap dan merespons `500` tanpa membocorkan stack trace ke client.
6. 📊 **Structured Logging & Observability** — Dilarang keras membiarkan blok `catch` kosong. Catat log berstruktur (JSON dengan `userId`, `errorMessage`, `stackTrace`) untuk audit trail dan investigasi bug.
7. 🔍 **Unambiguous Query Filtering Logic** — Logika query database (WHERE clause SQL/Prisma) WAJIB menangani data `NULL`/unassigned secara transparan (misal `WHERE label_id IS NULL`) agar data tidak hilang secara membingungkan saat pengguna memfilter.
8. **Security First** — Every endpoint is an attack surface. Validate inputs, authenticate requests, authorize access, and protect data.
9. **Fail Gracefully** — Systems will fail. Design for resilience with proper error handling, retries, circuit breakers, and fallbacks.
10. **Document Everything** — APIs, database schemas, architecture decisions, and deployment processes must be well-documented.
11. 📝 **5-Step T-C-R-E-I Prompting Framework** — Terapkan kerangka kerja 5 langkah (Task, Context, References, Evaluate, Iterate) untuk memformulasi instruksi dan arsitektur backend. Lihat `references/prompting-framework-guide.md`.

---

## Standard Tech Stack Guidelines

Setiap pengembangan Backend WAJIB mengacu pada stack standar berikut:

- ⚙️ **Server Framework**: Express JS (TypeScript / Node.js)
- 🗄️ **Database**: Supabase PostgreSQL
- 📦 **File & Media Storage**: Supabase Bucket Storage
- 🛠️ **ORM**: Prisma ORM (`prisma/schema.prisma` migrations & client)
- 🔐 **Authentication & Authorization**: Better Auth + JWT Token (Rotation & RBAC)
- 🌐 **Client Interoperability**:
  - **Next.js / React Clients**: Port `3000`
  - **Vue 3 SPA (Vite) Clients**: Port `5173`
  - **Nuxt 3 SSR Clients**: Port `3000`
  - **CORS Config**:
    ```typescript
    import cors from 'cors';
    app.use(cors({
      origin: ['http://localhost:3000', 'http://localhost:5173', process.env.CLIENT_URL || ''],
      credentials: true,
      methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE', 'OPTIONS'],
    }));
    ```
- 🚀 **Deployment**: Vercel / Railway / Docker Container
- 🌿 **Git Branching Strategy**: GitHub dengan `dev` branch (development) & `main` branch (production release)
- 🎬 **Motion Design**: Gunakan panduan LottieFiles motion design skill untuk keselarasan endpoint & state UI animation (loading, success, error feedback) dengan frontend.
- 🧊 **Three.js / 3D Asset Management**: Gunakan skill threejs-* (misal: @threejs-loaders, @threejs-geometry) jika backend bertugas memproses, memvalidasi, atau menyimpan aset 3D (GLTF/GLB) untuk di-serve ke frontend.
- 🧬 **Design DNA**: Gunakan skill @design-dna jika perlu mendesain database atau skema API untuk menyimpan konfigurasi tema/design tokens secara dinamis.
- 🎭 **E2E API & Auth Verification**: Gunakan @playwright-skill jika perlu memvalidasi cookie/session auth rotation dan alur API secara nyata end-to-end dari sisi client browser.
- 🎭 **Creative Code Sync**: Jika berinteraksi dengan antarmuka yang di-generate via @paint atau @cast (Genjutsu), pastikan payload API dioptimalkan agar tidak memblokir main thread UI selama animasi kompleks berlangsung.
- 🛡️ **Safe Logic Flow & Error Handling Guide**: Guard Clause, Result Pattern, Custom Exception, Global Error Handler & Structured Logging. Lihat `references/safe-logic-flow-guide.md`.
- 🗺️ **Maps & Routing Services**: Route API Proxy (sembunyikan API Key) atau Self-hosted OSRM Engine. Lihat `references/routing-and-maps-guide.md`.
- 🛠️ **Dynamic Master Data Schema & APIs**: Tabel dinamis & CRUD Admin API untuk data master. Lihat `references/dynamic-masterdata-and-flow-guide.md`.
- 📝 **Prompting Best Practices**: 5-Step T-C-R-E-I Framework (Task, Context, References, Evaluate, Iterate). Lihat `references/prompting-framework-guide.md`.
- ⏱️ **Supabase CronJob & Auth Guide**: Panduan implementasi cron job keep-alive dan keamanan data Supabase. Lihat `references/supabase-cronjob-guide.md`.

---

## Safe Logic Flow & Error Handling Architecture

Standar pengelolaan alur logika tanpa memicu *silent bug* dan tanpa membuat aplikasi *crash* secara liar:

### Ringkasan Alur Kerja Aman (*Architecture Flow*)

| Lapisan Kode (*Layer*) | Metode yang Digunakan | Perilaku Saat Terjadi Kondisi Gagal |
| --- | --- | --- |
| **Validation / Input** | `if-else` / Guard Clause / Zod | Kembalikan respons validasi `400 Bad Request` ke pengguna. |
| **Business Logic (Service)** | Result Pattern & Domain Exception | Kembalikan `Result.fail()` untuk kegagalan bisnis, atau lempar `CustomException`. |
| **Infrastructure (DB / API)** | `try-catch` + Structured Logging | Tangkap error teknis, buat log detail, lalu *re-throw* atau bungkus dengan `CustomException`. |
| **Outer Layer (Framework)** | Global Exception Handler | Menangkap semua error yang lolos, menyembunyikan stack trace dari pengguna akhir, dan mengirim respons `500`. |

### Detail 5 Pola Utama:

1. **Pola Guard Clause (Early Return)**: Validasi prasyarat di baris awal fungsi. Langsung `return` jika kondisi tidak terpenuhi.
2. **Result Pattern (Result Object)**: Kembalikan objek `{ isSuccess, data, error }` pada Service layer untuk kegagalan bisnis biasa (misal email sudah terdaftar).
3. **Custom Domain Exception**: Buat turunan `Error` khusus (misal `InsufficientBalanceException`) untuk membedakan error domain vs error sistem.
4. **Centralized Global Exception Handler**: Tangkap unhandled exception di Middleware/Filter Express, log stack trace, return HTTP `500` yang aman dan ramah pengguna.
5. **Structured Logging & Observability**: Dilarang membiarkan `catch` kosong. Log detail konteks (`userId`, `errorMessage`, `stackTrace`).

Lihat `references/safe-logic-flow-guide.md` untuk rincian pola dan contoh kode lengkap.

---

## Capabilities

This Backend skill covers **6 core areas**. When invoked, determine which area(s) are relevant based on the user's request.

### 1. API Design
- **RESTful Conventions**: Resource naming, HTTP methods, status codes, URL structure
- **Request/Response Patterns**: Envelope patterns `{ isSuccess, data, error }`, pagination metadata
- **Frontend Interop**: Standardized contracts for React / Vue 3 Pinia / Nuxt 3 composables
- **Documentation**: OpenAPI/Swagger specifications

See `references/api-design-guide.md`.

### 2. Database Management
- **Schema Design**: Normalization (3NF), data types, foreign key constraints
- **Indexing & Optimization**: Composite indexes, EXPLAIN analysis, N+1 prevention
- **Migrations & ORM**: Prisma ORM, safe migrations, connection pooling

See `references/database-patterns.md`.

### 3. Authentication & Authorization
- **JWT & OAuth 2.0**: Access/refresh tokens, token rotation, RBAC/ABAC
- **Session & Cookie Security**: HttpOnly, SameSite, Secure flags for SPA & SSR clients

See `references/auth-patterns.md`.

### 4. Architecture Patterns
- **Layered Architecture**: Controller → Service → Repository → Data Source
- **Dependency Injection**: IoC containers, constructor injection
- **Clean Architecture & DDD**: Use cases, domain events, bounded contexts

See `references/architecture-guide.md` and `references/js-at-scale-backend.md`.

### 5. Error Handling & Observability
- **Guard Clause & Result Pattern**: Early return, explicit result status
- **Custom Exceptions**: Domain error hierarchy vs system errors
- **Global Error Handler**: Framework-level exception middleware, sanitized 500 responses
- **Structured Logging**: JSON logger (Winston/Pino), correlation IDs, non-empty catch blocks

See `references/safe-logic-flow-guide.md`.

### 6. Deployment & DevOps
- **Docker & CI/CD**: Multi-stage Dockerfile, automated test/deploy pipelines
- **Graceful Shutdown & Probes**: Liveness/readiness probes, connection draining

---

## Backend Development Workflow

### Phase 1: Understand & Plan
1. Clarify requirements, business rules, and API contracts
2. Identify domain models and master data requirements (Zero hardcoded master data)

### Phase 2: Architecture & Schema
1. Design database schema with Prisma ORM (foreign keys, indexes)
2. Define API endpoints, request validation, and Result pattern structures

### Phase 3: Implement Safe Logic & APIs
1. Apply Guard Clause for input validation in Controllers/Services
2. Use Result Pattern in Service layer methods
3. Throw Custom Domain Exceptions for business rule breaches
4. Wrap infrastructure calls with `try-catch` and structured logging
5. Wire Centralized Global Error Handler Middleware

### Phase 4: Validate & Deploy
1. Test unit/integration error flows and 400/500 HTTP responses
2. Verify CORS and Authentication compatibility with client frameworks (Next.js, Vue 3, Nuxt 3)
