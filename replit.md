# Corporate Ledger (CLEG) - Real Estate Tokenization Platform

## Overview

Corporate Ledger (CLEG) is a blockchain-based platform for tokenizing high-end commercial real estate properties in Brazil. The platform enables fractional ownership of commercial buildings through digital tokens, providing liquidity and transparency to traditionally illiquid real estate investments. Users can browse tokenized properties, purchase tokens starting at R$ 5,000, track their portfolio, and receive automated yield distributions.

The application is a full-stack web platform built with a modern React frontend and Express.js backend, following a mobile-first responsive design approach with a futuristic FinTech aesthetic.

## Current Status

**Production-Ready Backend Infrastructure Complete (October 28, 2025)** ✅

All core features with production-grade backend:
- ✅ Complete landing page with hero, benefits, process flow, and market data
- ✅ Marketplace displaying 6 tokenized commercial properties
- ✅ **PostgreSQL database** with persistent data storage (via Neon Serverless)
- ✅ **Real authentication system** with bcrypt password hashing
- ✅ **Session-based auth** with PostgreSQL session store (connect-pg-simple)
- ✅ **Protected routes** requiring authentication (purchase, portfolio)
- ✅ Full token purchase workflow with real user separation
- ✅ User dashboard with portfolio visualization and yield tracking
- ✅ Authentication pages with auto-login after registration
- ✅ Dark/light theme toggle with persistence
- ✅ Fully responsive mobile design
- ✅ End-to-end tests passing (registration → purchase → portfolio)

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Tooling:**
- React 18 with TypeScript for type safety
- Vite as the build tool for fast development and optimized production builds
- Wouter for client-side routing (lightweight alternative to React Router)
- TanStack Query (React Query) for server state management and data fetching

**UI Component System:**
- Shadcn/ui component library built on Radix UI primitives
- Tailwind CSS for utility-first styling with custom design tokens
- Custom theme system supporting dark/light modes
- Design follows "New York" style variant from Shadcn/ui

**Design System:**
- Futuristic FinTech aesthetic with blockchain visual language
- Primary colors: Dark Navy Blue (#0A1128), Graphite Gray (#2C3E50)
- Accent colors: Electric Green/Cyan (#00FFC2, #00C2FF)
- Typography: Montserrat for headings, Inter/Roboto for body text
- Mobile-first responsive design with consistent spacing rhythm

**Key Pages:**
- Landing page (`/`) with hero section and benefits showcase
- Assets listing (`/ativos`) displaying available tokenized properties
- User dashboard (`/dashboard`) showing portfolio and yields
- Authentication (`/login`) with tabs for login/registration
- Static pages for whitepaper and contact

**State Management:**
- TanStack Query for server state (assets, portfolio, yields)
- React Context for theme preferences
- Local component state with React hooks
- Form state managed by React Hook Form with Zod validation

### Backend Architecture

**Framework:**
- Express.js server running on Node.js
- TypeScript for type safety across frontend and backend
- ESM modules throughout the codebase

**API Design:**
- RESTful API structure under `/api` prefix
- Session-based authentication with PostgreSQL session store
- JSON request/response format
- Centralized error handling
- Protected routes via requireAuth middleware

**Key API Endpoints:**
- `POST /api/auth/register` - User registration with auto-login (password hashed)
- `POST /api/auth/login` - User authentication with bcrypt password verification
- `POST /api/auth/logout` - Session destruction
- `GET /api/auth/me` - Get authenticated user data (protected)
- `GET /api/assets` - Fetch all tokenized assets (public)
- `POST /api/assets/:id/purchase` - Purchase asset tokens (protected, requires auth)
- `GET /api/user/portfolio` - Fetch user's portfolio and yields (protected, requires auth)

**Data Storage:**
- PostgreSQL database via Neon Serverless (@neondatabase/serverless)
- PostgreStorage implementation (server/postgres-storage.ts)
- Database schema defined using Drizzle ORM
- Schema includes: users, assets, user_portfolios, yields, session tables
- Database seeding script (server/seed.ts) with 6 commercial building assets

**Storage Layer Pattern:**
- Interface-based design (`IStorage`) for storage abstraction
- PostgreStorage implementation using Drizzle ORM
- All data persists across server restarts
- Pre-seeded with 6 sample commercial building assets via seed script

### Data Schema

**Users Table:**
- id: varchar (UUID primary key, auto-generated)
- email: varchar (unique)
- password: varchar (bcrypt hashed, 10 salt rounds)
- name: varchar

**Assets Table:**
- id: varchar (UUID primary key, auto-generated)
- name: varchar (e.g., "Edifício Corporate Plaza")
- location: varchar (e.g., "São Paulo, SP")
- description: text
- tokenPrice: integer (R$ 5.000 per token)
- totalTokens: integer (1.000 tokens per asset)
- remainingTokens: integer (decreases with each purchase)
- estimatedApy: varchar (e.g., "12%")
- imageUrl: varchar

**User Portfolios Table:**
- id: varchar (UUID primary key, auto-generated)
- userId: varchar (FK to users.id)
- assetId: varchar (FK to assets.id)
- quantity: integer (number of tokens owned)
- purchasePrice: integer (price paid per token)
- purchaseDate: timestamp

**Yields Table:**
- id: varchar (UUID primary key, auto-generated)
- userId: varchar (FK to users.id)
- assetId: varchar (FK to assets.id)
- amount: integer (yield amount in R$)
- date: timestamp

**Session Table:**
- sid: varchar (primary key, session ID)
- sess: json (session data)
- expire: timestamp (session expiration)

### Authentication & Session Management

**Authentication Flow:**
- Email/password authentication with bcrypt password hashing
- Sessions stored in PostgreSQL via connect-pg-simple
- Session-based auth (no JWT tokens)
- Session persistence across requests via httpOnly cookies
- Auto-login after registration (session created immediately)

**Security Implementation:**
- ✅ Passwords hashed with bcrypt (10 salt rounds) before storage
- ✅ Sessions persisted in PostgreSQL (survive server restarts)
- ✅ httpOnly cookies prevent XSS attacks
- ✅ secure flag enabled in production
- ✅ sameSite: 'lax' prevents CSRF attacks
- ✅ 30-day session expiration (maxAge: 30 days)
- ✅ requireAuth middleware protects sensitive routes
- ✅ SESSION_SECRET environment variable for production

**Protected Routes:**
- POST /api/assets/:id/purchase - Requires authenticated session
- GET /api/user/portfolio - Requires authenticated session
- GET /api/auth/me - Requires authenticated session

### Development Environment

**Hot Module Replacement:**
- Vite dev server with HMR for instant updates
- Development-only error overlay plugin
- Replit-specific plugins for cartographer and dev banner

**Build Process:**
- Frontend: Vite builds to `dist/public`
- Backend: esbuild bundles server code to `dist`
- Separate dev and production modes
- TypeScript compilation checking via `tsc`

**Project Structure:**
- `/client` - Frontend React application
- `/server` - Backend Express server
- `/shared` - Shared TypeScript types and schemas
- `/attached_assets` - Static assets (images, design docs)

## External Dependencies

### Third-Party Services

**Database:**
- PostgreSQL via Neon Serverless (@neondatabase/serverless)
- Connection string required via `DATABASE_URL` environment variable
- Drizzle ORM for schema definition and migrations

**UI Component Libraries:**
- Radix UI primitives for accessible components
- Recharts for data visualization (portfolio charts)
- Lucide React for icon system
- Embla Carousel for image carousels

**Form Handling:**
- React Hook Form for form state management
- Zod for runtime schema validation
- @hookform/resolvers for Zod integration

**Development Tools:**
- Replit-specific Vite plugins for development experience
- PostCSS with Tailwind and Autoprefixer
- TypeScript for type checking across the stack

**Font Hosting:**
- Google Fonts (Montserrat and Inter families)
- Preconnect optimization in HTML

### API & Integration Notes

**Session Management:**
- Uses `connect-pg-simple` package (prepared for PostgreSQL sessions)
- Currently implements simple in-memory Map
- Ready for migration to persistent session store

**Image Assets:**
- Generated building images stored in `/attached_assets/generated_images`
- Served statically via Vite's asset handling
- Blockchain background patterns for visual theming

**Build & Deployment:**
- Production build requires both frontend (Vite) and backend (esbuild) compilation
- Environment variable `DATABASE_URL` must be set for database connection
- Node environment detection via `NODE_ENV`

## Recent Changes

### October 28, 2025 - Production Infrastructure Upgrade

**✅ Task 1: Database Setup & Migration (COMPLETED)**
- Migrated from in-memory storage (MemStorage) to PostgreSQL database
- Created database schema using Drizzle ORM with all tables (users, assets, user_portfolios, yields, session)
- Implemented PostgreStorage class (server/postgres-storage.ts) with full CRUD operations
- Created database seeding script (server/seed.ts) with 6 commercial property assets
- All data now persists across server restarts via Neon Serverless connection

**✅ Task 2: Real Authentication System (COMPLETED)**
- Implemented bcrypt password hashing (10 salt rounds) via hashPassword/comparePassword functions
- Migrated from in-memory sessions to PostgreSQL session store using connect-pg-simple
- Created requireAuth middleware to protect sensitive routes
- Added authentication endpoints:
  - POST /api/auth/register - Creates user with hashed password, auto-login via session
  - POST /api/auth/login - Validates bcrypt password hash, creates session
  - POST /api/auth/logout - Destroys session correctly
  - GET /api/auth/me - Returns authenticated user data
- Session configuration: 30-day maxAge, httpOnly cookies, secure in production, sameSite: 'lax'
- Extended Express types to support req.session.userId and req.userId

**✅ Task 3: Complete Token Purchase Flow (COMPLETED)**
- Updated POST /api/assets/:id/purchase to require authentication (requireAuth middleware)
- Removed hardcoded "demo-user-id" - now uses real userId from authenticated session
- Updated GET /api/user/portfolio to require authentication and use session userId
- Frontend login page now redirects to dashboard after registration (auto-login)
- Purchase modal correctly invalidates caches after successful purchase
- All user data properly separated - each user has their own portfolio and yields

**End-to-End Testing:**
- Complete test validated: registration → auto-login → navigate to assets → purchase 2 tokens → verify dashboard updated → logout
- Test confirmed: Total Investido R$ 10.000, Total de Tokens 2, remainingTokens correctly updated (848/1000)
- All data persisted correctly in PostgreSQL database
- Zero hardcoded user IDs - full multi-user support working

**Architecture Changes:**
- Removed MemStorage completely from codebase
- All routes now use PostgreStorage instance
- Database connection via DATABASE_URL environment variable
- Session table auto-managed by connect-pg-simple
- TypeScript session augmentation in server/index.ts

**Design System:**
- Primary accent: Electric Cyan (#00FFC2) for CTAs and highlights
- Dark navy background (#0A1128) in dark mode
- Graphite gray (#2C3E50) for secondary elements
- Blockchain-inspired visual elements (hexagons, network patterns)
- Montserrat headings + Inter body text
- Fully responsive with mobile-first approach
- hover-elevate and active-elevate-2 utility classes for interactions

## Next Steps (Roadmap)

**Priority Features (Task List):**
- ✅ Task 1: Database Setup & Migration - COMPLETED
- ✅ Task 2: Real Authentication System - COMPLETED  
- ✅ Task 3: Complete Token Purchase Flow - COMPLETED
- ⏳ Task 4: Contact Form Implementation
- ⏳ Task 5: Payment Integration (Stripe)
- ⏳ Task 6: KYC/Compliance Verification System
- ⏳ Task 7: Secondary Market (P2P Token Trading)
- ⏳ Task 8: Advanced Analytics & Performance Charts
- ⏳ Task 9: Blockchain Integration (Testnet)
- ⏳ Task 10: Automated Yield Distribution

**Infrastructure Improvements:**
- Add database transaction support for purchase flow (atomic operations)
- Implement rate limiting on auth and purchase endpoints
- Add Redis caching layer for frequently accessed data
- Database connection pooling optimization
- Comprehensive error logging and monitoring

**Security Enhancements:**
- CSRF protection tokens
- API rate limiting per user
- Input sanitization and SQL injection prevention
- Security headers (helmet.js)
- Two-factor authentication (2FA) option

**UX/UI Improvements:**
- Loading skeletons and better loading states
- Error boundaries with user-friendly messages
- Enhanced form validation feedback
- Accessibility improvements (ARIA labels, keyboard navigation)
- Onboarding tour for first-time users
- Real-time notifications for yield distributions

**Deployment Considerations:**
- Configure SESSION_SECRET in production environment
- Set up database backups and recovery procedures
- Implement CI/CD pipeline
- Performance monitoring and analytics
- Error tracking (Sentry or similar)