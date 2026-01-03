---
project: OpenCut
stars: 44783
description: The open-source CapCut alternative
url: https://github.com/OpenCut-app/OpenCut
---

OpenCut
=======

### A free, open-source video editor for web, desktop, and mobile.

Why?
----

-   **Privacy**: Your videos stay on your device
-   **Free features**: Every basic feature of CapCut is paywalled now
-   **Simple**: People want editors that are easy to use - CapCut proved that

Features
--------

-   Timeline-based editing
-   Multi-track support
-   Real-time preview
-   No watermarks or subscriptions
-   Analytics provided by Databuddy, 100% Anonymized & Non-invasive.
-   Blog powered by Marble, Headless CMS.

Project Structure
-----------------

-   `apps/web/` – Main Next.js web application
-   `src/components/` – UI and editor components
-   `src/hooks/` – Custom React hooks
-   `src/lib/` – Utility and API logic
-   `src/stores/` – State management (Zustand, etc.)
-   `src/types/` – TypeScript types

Getting Started
---------------

### Prerequisites

Before you begin, ensure you have the following installed on your system:

-   Node.js (v18 or later)
-   Bun (for `npm` alternative)
-   Docker and Docker Compose

> **Note:** Docker is optional, but it's essential for running the local database and Redis services. If you're planning to run the frontend or want to contribute to frontend features, you can skip the Docker setup. If you have followed the steps below in Setup, you're all set to go!

### Setup

1.  Fork the repository
    
2.  Clone your fork locally
    
3.  Navigate to the web app directory: `cd apps/web`
    
4.  Copy `.env.example` to `.env.local`:
    
    # Unix/Linux/Mac
    cp .env.example .env.local
    
    # Windows Command Prompt
    copy .env.example .env.local
    
    # Windows PowerShell
    Copy-Item .env.example .env.local
    
5.  Install dependencies: `bun install`
    
6.  Start the development server: `bun dev`
    

Development Setup
-----------------

### Local Development

1.  Start the database and Redis services:
    
    # From project root
    docker-compose up -d
    
2.  Navigate to the web app directory:
    
    cd apps/web
    
3.  Copy `.env.example` to `.env.local`:
    
    # Unix/Linux/Mac
    cp .env.example .env.local
    
    # Windows Command Prompt
    copy .env.example .env.local
    
    # Windows PowerShell
    Copy-Item .env.example .env.local
    
4.  Configure required environment variables in `.env.local`:
    
    **Required Variables:**
    
    # Database (matches docker-compose.yaml)
    DATABASE\_URL="postgresql://opencut:opencutthegoat@localhost:5432/opencut"
    
    # Generate a secure secret for Better Auth
    BETTER\_AUTH\_SECRET="your-generated-secret-here"
    BETTER\_AUTH\_URL="http://localhost:3000"
    
    # Redis (matches docker-compose.yaml)
    UPSTASH\_REDIS\_REST\_URL="http://localhost:8079"
    UPSTASH\_REDIS\_REST\_TOKEN="example\_token"
    
    # Marble Blog
    MARBLE\_WORKSPACE\_KEY=cm6ytuq9x0000i803v0isidst # example organization key
    NEXT\_PUBLIC\_MARBLE\_API\_URL=https://api.marblecms.com
    
    # Development
    NODE\_ENV="development"
    
    **Generate BETTER\_AUTH\_SECRET:**
    
    # Unix/Linux/Mac
    openssl rand -base64 32
    
    # Windows PowerShell (simple method)
    \[System.Web.Security.Membership\]::GeneratePassword(32, 0)
    
    # Cross-platform (using Node.js)
    node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
    
    # Or use an online generator: https://generate-secret.vercel.app/32
    
5.  Run database migrations: `bun run db:migrate` from (inside apps/web)
    
6.  Start the development server: `bun run dev` from (inside apps/web)
    

The application will be available at http://localhost:3000.

Contributing
------------

We welcome contributions! While we're actively developing and refactoring certain areas, there are plenty of opportunities to contribute effectively.

**🎯 Focus areas:** Timeline functionality, project management, performance, bug fixes, and UI improvements outside the preview panel.

**⚠️ Avoid for now:** Preview panel enhancements (fonts, stickers, effects) and export functionality - we're refactoring these with a new binary rendering approach.

See our Contributing Guide for detailed setup instructions, development guidelines, and complete focus area guidance.

**Quick start for contributors:**

-   Fork the repo and clone locally
-   Follow the setup instructions in CONTRIBUTING.md
-   Create a feature branch and submit a PR

Sponsors
--------

* * *

License
-------

MIT LICENSE

* * *
