# PC Club Time Calculator

## Overview

A web-based time and pricing calculator designed for PC club administrators. The application automatically detects weekday/weekend pricing, provides real-time cost calculations based on different tariff plans, and features a gaming-inspired dark-mode interface optimized for dimly lit environments. Built as a single-page application with a focus on instant clarity and minimal interaction friction.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework & Tooling**
- **React 18** with TypeScript for type-safe component development
- **Vite** as the build tool and development server, providing fast HMR and optimized production builds
- **Wouter** for lightweight client-side routing (chosen over React Router for smaller bundle size)
- **TanStack Query** for server state management and caching (with infinite stale time for static tariff data)

**UI Component System**
- **shadcn/ui** component library (New York style variant) built on Radix UI primitives
- **Tailwind CSS** for utility-first styling with custom design tokens
- **CVA (Class Variance Authority)** for type-safe component variant management
- Dark-first design system with gaming-inspired aesthetics using Inter and JetBrains Mono fonts

**State Management**
- Local component state for calculator inputs and selections
- Real-time clock updates using React useEffect intervals
- No global state management (Redux/Zustand) - keeping it simple with local state

**Design Decisions**
- Gaming-inspired minimalism with strategic visual elements
- High contrast dark theme for PC club environments
- Typography hierarchy using Inter for UI text and JetBrains Mono for numbers/prices
- Spacing system based on Tailwind's 4px grid (units: 2, 4, 6, 8, 12, 16)

### Backend Architecture

**Server Framework**
- **Express.js** with TypeScript running on Node.js
- ESM module system throughout the codebase
- Minimal API surface - primarily serves the React SPA

**Build & Deployment**
- Development: tsx for TypeScript execution without compilation
- Production: esbuild bundles the server code into ESM format
- Vite builds the client into `dist/public`
- Single process serves both static assets and any API endpoints

**Data Layer**
- **Drizzle ORM** configured for PostgreSQL (via `@neondatabase/serverless` driver)
- Schema defined in `shared/schema.ts` using Zod for validation
- Tariff data currently defined as static constants in shared schema
- Session management using `connect-pg-simple` for PostgreSQL-backed sessions

**Architectural Choices**
- Shared TypeScript types between client and server via `shared/` directory
- Path aliases configured (`@/`, `@shared/`, `@assets/`) for clean imports
- Database migrations managed through Drizzle Kit in `migrations/` folder
- Environment-based configuration with `DATABASE_URL` required for Postgres connection

### Data Models

**Tariff Schema**
```typescript
{
  id: string,
  name: string (English),
  nameRu: string (Russian),
  duration: number (minutes),
  description?: string,
  priceWeekday: number,
  priceWeekend: number,
  availableFrom?: number (hour),
  availableTo?: number (hour),
  perMinute: boolean (default: false)
}
```

**Pricing Logic**
- Weekend detection based on JavaScript Date day of week (0=Sunday, 6=Saturday)
- Time-based availability filtering using current hour
- Per-minute vs. fixed-duration tariff calculation
- Real-time price updates as user enters time values

### External Dependencies

**Database**
- **Neon PostgreSQL** (serverless Postgres) via `@neondatabase/serverless`
- Connection pooling and edge-compatible driver for modern deployment
- Drizzle ORM for type-safe database queries and schema management

**UI Component Libraries**
- **Radix UI** primitives (accordion, dialog, dropdown, popover, etc.) for accessible components
- **lucide-react** for consistent icon set throughout the UI
- **date-fns** for date formatting and manipulation
- **embla-carousel-react** for carousel functionality (if needed for tariff display)

**Form Management**
- **react-hook-form** with **@hookform/resolvers** for form validation
- **zod** for runtime schema validation (shared with Drizzle)
- **drizzle-zod** for generating Zod schemas from Drizzle tables

**Styling & Utilities**
- **tailwindcss** with **autoprefixer** via PostCSS
- **clsx** and **tailwind-merge** (via `cn` utility) for conditional class merging
- **class-variance-authority** for component variant management

**Development Tools**
- **@replit/vite-plugin-runtime-error-modal** for better error visibility during development
- **@replit/vite-plugin-cartographer** and **dev-banner** for Replit-specific tooling (development only)
- TypeScript strict mode enabled for maximum type safety

**Session Management**
- **express-session** implied by use of `connect-pg-simple`
- PostgreSQL-backed session store for persistent sessions across restarts

**Key Design Trade-offs**
1. Static tariff data in code vs. database: Chose code-based for simplicity and type safety, can migrate to DB later if dynamic tariff management is needed
2. Minimal backend: No complex API routes currently, primarily serving the SPA - can expand as needed
3. Dark-first only: No light mode toggle to reduce complexity and maintain focused gaming aesthetic
4. Russian + English labels: Dual language support built into tariff schema for localization