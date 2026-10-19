# Digvijay Shingare — Full-Stack Portfolio Platform

A production-grade, feature-rich portfolio and learning platform built with React, Node.js, Supabase, and Upstash Redis. This is not a static portfolio — it is a complete web application with a quiz engine, notes library, daily coding challenges, a community forum, a resume builder, and a full administrative dashboard.

---

## Live Preview

<img width="2962" alt="Home Page" height="1648" alt="Image" src="https://github.com/user-attachments/assets/c5444bcf-1c50-4856-8910-672c8a975ecc" />


---

## Table of Contents

- [Overview](#overview)
- [Feature Showcase](#feature-showcase)
- [Technical Architecture](#technical-architecture)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Database Setup](#database-setup)
- [API Reference](#api-reference)
- [Admin Dashboard](#admin-dashboard)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

This platform combines a personal portfolio with a fully functional learning community. Visitors can browse projects, read technical content, take quizzes to earn coins, download study notes, participate in a community forum, solve daily coding challenges, and build and download professional resumes — all in a single application.

The admin (portfolio owner) has complete control over all content through a dedicated dashboard that manages projects, notes, quizzes, skills, certificates, bookmarks, timeline entries, and platform settings without touching code.

---

## Feature Showcase

### Public Portfolio

<img width="2896" alt="About Page" height="1646" alt="Image" src="https://github.com/user-attachments/assets/afc9e608-910f-48f2-b94e-1562fb393a08" />

The portfolio consists of a landing page, an about section with animated skill proficiency bars, a projects gallery with filtering, a work experience and education timeline, certificates, and a contact form that delivers messages to the admin email.

---

### Admin Dashboard

<img width="3024" alt="Admin Overview" src="https://github.com/user-attachments/assets/6e9649eb-0308-4ed9-9dd2-6970068dfd43" />

The admin dashboard provides a comprehensive overview of platform activity including total users, quizzes played, notes downloaded, and coins in circulation. All content on the platform is managed from this single interface.

---

### Analytics

<img width="2984" alt="Admin Analytics" src="https://github.com/user-attachments/assets/3bd520d2-0ba8-4e2f-8fc2-f7d8d03f9a67" />

Real-time analytics track page views, unique visitors, average session duration, bounce rate, top pages, device distribution, and visitor geography. Data is visualised with custom SVG charts built without external chart libraries.

---

### Platform Settings

<img width="3014" alt="Settings" src="https://github.com/user-attachments/assets/f47992c3-f178-4de0-9a6a-69ac6319645b" />

Platform-level configuration including feature flag toggles (community forum, quiz platform, notes library, analytics, daily login bonus, leaderboard), coin reward amounts, and rate limiting — all managed without redeployment.

---

### Daily Coding Challenges

<img width="2850" alt="Daily Challenges" src="https://github.com/user-attachments/assets/1593b048-4f56-41ba-adef-d04a87a66e35" />

A daily coding challenge system with a browser-based Monaco editor, multi-language support (Java, Python, JavaScript, C++, Docker commands, Kubernetes commands), and automatic test case grading via the JDoodle execution engine. Users earn coins on first solve, pay a reattempt fee on subsequent attempts, and build daily streaks. Previous submissions are auto-loaded in the editor.

---

### Notes Library

<img width="2742" alt="Notes Library" src="https://github.com/user-attachments/assets/5f2b23ff-d79d-473d-a5ba-b8f8a6604953" />

A coin-gated study materials library. Users spend coins to download PDF, DOC, DOCX, and presentation files uploaded by the admin. Files are stored on Supabase Storage with public access URLs. Users can preview documents before purchasing.

---

## Technical Architecture

```
client/                     React 18 SPA (Vite)
  src/
    components/             Reusable UI components
    pages/                  Route-level page components
      admin/tabs/           All 13 admin dashboard tabs
      resume/               Resume builder with 3 templates
    services/               Axios-based API service layer
    store/                  Zustand global state stores
    mock/                   Mock data for development mode
    utils/                  Utilities (toast, bell sound, etc.)

server/                     Node.js + Express API
  routes/                   Route handlers (REST endpoints)
  controllers/              Business logic
  middleware/               JWT auth, rate limiting, file upload
  config/                   Supabase, Redis, env, app.yaml
  utils/                    Logger, notification helper

database/
  schema.sql                Full PostgreSQL schema (Supabase)
  migration_v2.sql          Column additions and new tables
  migration_v3.sql          Daily challenges tables
```

---

## Technology Stack

### Frontend

| Technology | Purpose |
|---|---|
| React 18 | UI framework with concurrent features |
| Vite | Build tool and development server |
| TailwindCSS | Utility-first styling with custom design tokens |
| Framer Motion | Page transitions, scroll animations, spring physics |
| @monaco-editor/react | VS Code editor embedded in the challenge page |
| @tanstack/react-query | Server state management, caching, background refetch |
| Zustand | Client state management (auth, theme, coins, notifications) |
| react-markdown + remark-gfm | Markdown rendering in community forum |
| html2canvas + jsPDF | Resume PDF export from rendered DOM |
| docx | Resume Word document generation |
| react-icons / lucide-react | Icon systems |

### Backend

| Technology | Purpose |
|---|---|
| Node.js 18 + Express | REST API server |
| Supabase | PostgreSQL database + file storage + auth helpers |
| Upstash Redis | Caching, rate limiting, refresh token storage, session data |
| jsonwebtoken + bcryptjs | JWT authentication and password hashing |
| multer | Multipart file upload handling |
| nodemailer | Contact form and OTP email delivery |
| socket.io | Real-time quiz and community features |
| JDoodle API | Code execution engine for daily challenges |

---

## Project Structure

```
Portfolio/
├── client/                 React frontend (Vite)
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Landing.jsx
│   │   │   ├── About.jsx
│   │   │   ├── Projects.jsx
│   │   │   ├── Timeline.jsx
│   │   │   ├── Certificates.jsx
│   │   │   ├── Notes.jsx
│   │   │   ├── Quiz.jsx
│   │   │   ├── Bookmarks.jsx
│   │   │   ├── Challenges.jsx
│   │   │   ├── Community.jsx
│   │   │   ├── UserDashboard.jsx
│   │   │   ├── ForgotPassword.jsx
│   │   │   ├── resume/
│   │   │   │   ├── ResumeBuilder.jsx
│   │   │   │   ├── JakesTemplate.jsx
│   │   │   │   ├── ModernTemplate.jsx
│   │   │   │   └── MinimalTemplate.jsx
│   │   │   └── admin/
│   │   │       └── tabs/ (13 admin management tabs)
│   │   ├── components/
│   │   │   ├── layout/     Navbar, Footer, ThemeToggle
│   │   │   └── ui/         SearchBar, MarkdownEditor, NotifPopup, etc.
│   │   ├── services/       API service layer per feature
│   │   ├── store/          Zustand stores (auth, coins, theme, notifications, settings)
│   │   └── utils/          toast.js, bellSound.js, animations.js
│   └── vite.config.js
│
├── server/
│   ├── routes/             One file per resource domain
│   ├── controllers/        auth, coins, community, notes, quiz, portfolio
│   ├── middleware/         verifyJWT, requireAdmin, rateLimiter, upload
│   ├── config/             db.js, redis.js, env.js, app.yaml, appConfig.js
│   └── utils/              logger.js, notify.js
│
└── database/
    ├── schema.sql
    ├── migration_v2.sql
    └── migration_v3.sql
```

---

## Getting Started

### Prerequisites

- Node.js 18 or higher
- A [Supabase](https://supabase.com) project
- An [Upstash Redis](https://upstash.com) database
- A [JDoodle](https://jdoodle.com) account (for code execution)

### Installation

```bash
# Clone the repository
git clone https://github.com/digvijay-shingare/portfolio.git
cd portfolio

# Install server dependencies
cd server
npm install

# Install client dependencies
cd ../client
npm install
```

### Running in Development

```bash
# Start the API server (from /server)
npm run dev

# Start the frontend (from /client)
npm run dev
```

The frontend will be available at `http://localhost:5173` and the API at `http://localhost:5000`.

---

## Environment Variables

Create `server/.env` with the following variables:

```env
PORT=5000
NODE_ENV=development

# Supabase — https://app.supabase.com/project/<id>/settings/api
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-service-role-key

# Upstash Redis — https://console.upstash.com
UPSTASH_REDIS_REST_URL=https://your-redis.upstash.io
UPSTASH_REDIS_REST_TOKEN=your-token

# JWT secret (generate with: openssl rand -base64 32)
JWT_SECRET=your-secret

# CORS origin
CLIENT_URL=http://localhost:5173

# Email (Gmail App Password for contact form and OTP emails)
GMAIL_USER=your-email@gmail.com
GMAIL_PASS=your-app-password
ADMIN_EMAIL=your-email@gmail.com

# Code execution engine — https://jdoodle.com/compiler-api
JDOODLE_CLIENT_ID=your-client-id
JDOODLE_CLIENT_SECRET=your-client-secret
```

Create `client/.env`:

```env
VITE_API_URL=http://localhost:5000/api
VITE_SOCKET_URL=http://localhost:5000
```

---

## Database Setup

Run the SQL files in order in the Supabase SQL Editor:

```
1. database/schema.sql          — Core tables
2. database/migration_v2.sql    — Extended columns and new feature tables
3. database/migration_v3.sql    — Daily challenges tables
```

Create the following Supabase Storage buckets:
- `images` (public) — profile photos, project images, certificate files
- `files` (public) — notes, documents

After running the schema, register via the API and then set your account role to `ADMIN` in the Supabase Table Editor.

---

## API Reference

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register a new account |
| POST | `/api/auth/login` | Login and receive JWT |
| POST | `/api/auth/logout` | Invalidate refresh token |
| POST | `/api/auth/refresh` | Refresh access token |
| GET | `/api/auth/me` | Get current user |
| POST | `/api/auth/forgot-password` | Send OTP to email |
| POST | `/api/auth/verify-otp` | Verify OTP, receive reset token |
| POST | `/api/auth/reset-password` | Set new password |

### Portfolio (Public)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/portfolio/theme` | Global theme configuration |
| GET | `/api/portfolio/about` | Profile, skills, certificates, achievements |
| GET | `/api/portfolio/projects` | Published projects |
| GET | `/api/portfolio/timeline` | Work experience and education |
| GET | `/api/portfolio/skills` | Skills with proficiency |
| GET | `/api/portfolio/certificates` | Certificates |
| GET | `/api/portfolio/settings` | Platform feature flags |
| POST | `/api/portfolio/contact` | Submit contact form |

### Platform (Authenticated)

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/quizzes` | List active quizzes |
| POST | `/api/quizzes/:id/submit` | Submit quiz answers |
| GET | `/api/notes` | List available notes |
| POST | `/api/notes/:id/download` | Download a note (deducts coins) |
| GET | `/api/coins/balance` | Current coin balance |
| GET | `/api/coins/history` | Transaction history |
| GET | `/api/coins/leaderboard` | Top users by coins |
| GET | `/api/notifications` | User notifications |
| GET | `/api/challenges` | Published challenges |
| POST | `/api/challenges/:id/run` | Execute code (JDoodle) |
| POST | `/api/challenges/:id/submit` | Grade solution against test cases |
| GET | `/api/community/posts` | Community forum posts |
| POST | `/api/community/posts` | Create a post |
| POST | `/api/community/posts/:id/reply` | Reply to a post |

---

## Admin Dashboard

The admin dashboard is accessible at `/admin` for accounts with `role = ADMIN`. It provides the following management interfaces:

| Tab | Manages |
|---|---|
| Overview | Platform activity summary and quick actions |
| Analytics | Page views, visitors, devices, countries |
| Profile | Personal information and profile photo |
| Appearance | Global theme colors, fonts, presets |
| Projects | Portfolio project entries |
| Quizzes | Quiz creation with questions, difficulty, rewards |
| Notes | File uploads with coin pricing |
| Certificates | Certificate management with file attachments |
| Timeline | Work experience and education entries |
| Bookmarks | Curated reading list |
| Challenges | Daily coding challenge scheduling |
| Skills | Skill categories and proficiency levels |
| Users | User management, coin grants, role assignment |
| Settings | Feature flags, reward configuration |

---

## Key Design Decisions

**Mock mode** — A development toggle switches all API calls to local mock data, allowing frontend development and UI testing without a running backend.

**Coin system** — All gamification (quizzes, notes, challenges) uses a single coin ledger with an append-only transaction history. The `users.coins` column is the source of truth for balance, updated atomically alongside ledger entries.

**Code execution** — Challenge solutions are proxied through the server to JDoodle rather than called from the browser directly, enabling rate limiting, input sanitisation, and consistent stdin/stdout handling across languages.

**Resume builder** — Three fully isolated template components (Jake's Classic, Modern, Minimal) accept a single `resumeData` prop. PDF export captures the template DOM at full 794px width in an off-screen container, bypassing the scaled preview to produce pixel-accurate output.

**Notifications** — Inserted directly into a Supabase table by server-side events (quiz completion, challenge solve, bookmark addition, community reply). The client polls every 30 seconds and marks all as read when the notification panel is opened.

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

Built by [Digvijay Shingare](https://github.com/digvijay-shingare)
