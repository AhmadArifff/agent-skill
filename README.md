# Agent Skill Repository ðŸš€

> **Comprehensive Custom AI Agent Skills** for Software Development Life Cycle (SDLC) â€” Product Management, Backend Engineering, Frontend Engineering, Quality Assurance, and Graphify Knowledge Graph.

Created and maintained by **Ahmad Arif**.

---

## ðŸ“š Included Custom Skills

This repository contains 5 production-grade AI Agent Skills:

| Skill | Role / Function | Key Capabilities & Architecture |
|---|---|---|
| ðŸ“‹ [**PM (Product Manager)**](./skills/pm) | Product Requirements & Architecture | â€¢ **Documentation Only (No Code Writing)**<br>â€¢ PRD Creation & Feature Breakdown (MoSCoW)<br>â€¢ Mandatory Admin/App Auth Planning<br>â€¢ Early QA Shift-Left Alignment<br>â€¢ Dynamic Master Data & Unambiguous Flow Design |
| âš™ï¸ [**Backend Engineer**](./skills/backend) | Server, API & Database | â€¢ **Express JS + Prisma ORM + Supabase DB & Storage**<br>â€¢ Better Auth + JWT Token Rotation & RBAC<br>â€¢ Centralized Global Error Handler & Custom Exceptions<br>â€¢ Safe Logic Flow (Guard Clause & Result Pattern)<br>â€¢ Route Proxy API for Maps (Google/Mapbox/OSRM) |
| ðŸŽ¨ [**Frontend Engineer**](./skills/frontend) | UI/UX & Client Applications | â€¢ **Next.js + PWA + Tailwind CSS + Zustand**<br>â€¢ **UI/UX Pro Max Design Intelligence** (50+ styles, 97 palettes, 57 font pairings)<br>â€¢ Component Setup: Shadcn UI + Untitled UI + Animate UI<br>â€¢ Animations: Framer Motion + AnimeJS<br>â€¢ **Device Priority**: ðŸ“± Mobile (HP) & Tablet/iPad â†’ ðŸ’» Desktop<br>â€¢ Protected Routes & Admin Auth Guard |
| ðŸ§ª [**QA (Quality Assurance)**](./skills/qa) | Testing, Security & Quality Audit | â€¢ Early PM-QA Shift-Left Alignment<br>â€¢ Zero Hardcode Master Data Audit<br>â€¢ Data Misconception & Edge Case Testing<br>â€¢ Security Audit (OWASP, Auth, RBAC, IDOR, API Key leaks)<br>â€¢ Unit & E2E Testing (Vitest, Playwright) |
| ðŸŒ [**Graphify**](./skills/graphify) | Knowledge Graph & Codebase Mapping | â€¢ Persistent Codebase Knowledge Graph<br>â€¢ God Nodes & Community Detection<br>â€¢ Query, Path Extraction & Codebase Explanations |

---

## ðŸ› ï¸ Standard Project Tech Stack

All skills are configured to work seamlessly together under this unified tech stack:

- ðŸ’» **Frontend**: Next.js (App Router) + PWA + Tailwind CSS + Zustand
- ðŸ§© **UI Components**: Shadcn UI (`npx shadcn@latest init`) + Untitled UI (`npx untitledui@latest init --nextjs`)
- ðŸŽ­ **Animations**: Framer Motion + AnimeJS (`npm install animejs`) + Animate UI (`npx shadcn@latest add @animate-ui/...`)
- âš™ï¸ **Backend**: Express JS (TypeScript / Node.js)
- ðŸ—„ï¸ **Database & Storage**: Supabase PostgreSQL + Supabase Bucket Storage
- ðŸ› ï¸ **ORM**: Prisma ORM (`prisma/schema.prisma`)
- ðŸ”’ **Auth & Security**: Better Auth + JWT Token (Access/Refresh Token Rotation)
- ðŸ—ºï¸ **Maps & Routing**: Google Maps Platform / Mapbox GL JS / OSRM + Leaflet / MapLibre
- ðŸŒ¿ **Git Workflow**: GitHub with `dev` branch (Development) & `main` branch (Production Release)
- ðŸš€ **Deployment**: Vercel
- ðŸ“ **Prompting Framework**: 5-Step T-C-R-E-I Framework (Task, Context, References, Evaluate, Iterate)

---

## ðŸ“ Repository Structure

```
agent-skill/
â”œâ”€â”€ README.md
â”œâ”€â”€ LICENSE
â”œâ”€â”€ skills/                      # Production Skill Folders
â”‚   â”œâ”€â”€ pm/                      # Product Manager Skill & Reference Guides
â”‚   â”œâ”€â”€ backend/                 # Backend Engineer Skill & Reference Guides
â”‚   â”œâ”€â”€ frontend/                # Frontend Engineer & UI/UX Pro Max Skill
â”‚   â”œâ”€â”€ qa/                      # Quality Assurance Skill & Reference Guides
â”‚   â””â”€â”€ graphify/                # Graphify Skill & Knowledge Graph Spec
â””â”€â”€ .agents/                     # Local Workspace Discovery Root
    â””â”€â”€ skills/
        â”œâ”€â”€ pm/
        â”œâ”€â”€ backend/
        â”œâ”€â”€ frontend/
        â”œâ”€â”€ qa/
        â””â”€â”€ graphify/
```

---

## ðŸš€ How to Install & Use

### Option 1: Global Installation (All Projects)
Copy the skills to your global agent config directory:

```bash
# Windows (PowerShell)
Copy-Item -Path ".\skills\*" -Destination "$env:USERPROFILE\.gemini\config\skills" -Recurse -Force
```

### Option 2: Workspace Installation (Single Project)
Copy the `.agents/skills` directory into your project workspace root:

```bash
# Copy to project workspace
cp -r .agents /path/to/your/project/
```

---

## ðŸ“„ License

This project is licensed under the **MIT License** â€” see the [LICENSE](./LICENSE) file for details.

Copyright (c) 2026 **Ahmad Arif**.


---

## External 3rd-Party Skills Integrated

This ecosystem has been enhanced with several powerful external skills sourced from GitHub. These skills are fully integrated into the core agents (/pm, /qa, /backend, /frontend):

| External Skill | Source | Purpose / Integration |
|---|---|---|
| **Motion Design** | LottieFiles/motion-design-skill | Standardizes easing, choreography, and motion personality across UI interactions. |
| **Three.js Skills** | pinkforest/threejs-playground | 10 specialized skills (@threejs-fundamentals, etc.) for 3D/WebGL rendering, asset management, and performance testing. |
| **Design DNA** | zanwei/design-dna | Extracts and enforces visual design identity (Design Tokens JSON) from reference images/screenshots. |
| **Genjutsu** | AThevon/genjutsu | Provides @cast for micro-interactions and @paint for full visual universe bootstrapping & audits. |

