# SecureShare - Secure File Transfer Application

## Overview

SecureShare is a full-stack file transfer web application that enables secure, temporary file sharing through 6-digit codes. Users can upload files or folders, set expiration times, add password protection, and limit download counts. Recipients retrieve files using the generated code and optional password. The application features QR code generation for easy sharing, automatic cleanup of expired transfers, and a modern, responsive UI.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Technology Stack:**
- React 18 with TypeScript
- Vite for build tooling and development server
- Wouter for client-side routing
- TanStack Query (React Query) for server state management
- Shadcn/ui component library with Radix UI primitives
- Tailwind CSS for styling

**Design System:**
- Material Design 3 (Modified) approach for utility-focused UI
- Dark mode as primary theme with light mode support
- Custom color palette based on trust and security (blue primary, clear status colors)
- Inter font for interface text, JetBrains Mono for codes and file sizes
- Component path aliases configured for clean imports (@/, @shared/, @assets/)

**State Management:**
- React Query for API data fetching and caching
- Local component state for UI interactions
- Theme context provider for dark/light mode toggle

**Key UI Components:**
- Upload view: Drag-and-drop file/folder upload with progress tracking
- Success view: Display 6-digit code, QR code, and sharing options
- Retrieve view: Code input (6 separate digit fields) with password protection
- File list view: Download individual files or as ZIP archive

### Backend Architecture

**Technology Stack:**
- Node.js with Express server
- TypeScript throughout
- PostgreSQL database via Neon serverless driver
- Drizzle ORM for database operations
- File-based storage strategy in development (MemStorage fallback)

**API Design:**
- RESTful endpoints under `/api` prefix
- Multer middleware for multipart file uploads
- File size limits configurable via environment variables (MAX_UPLOAD_SIZE_MB)
- Request/response logging middleware

**Core Routes:**
- POST `/api/transfers/upload` - File upload with metadata
- GET `/api/transfers/:code` - Retrieve transfer by code
- POST `/api/transfers/:code/verify` - Password verification
- GET `/api/transfers/:code/download/:fileId` - Download single file
- GET `/api/transfers/:code/download-zip` - Download as ZIP archive

**Database Schema (Drizzle + PostgreSQL):**
- `transfers` table: Stores transfer metadata (code, password hash, expiration, download limits)
- `transfer_files` table: Individual file records linked to transfers
- UUID primary keys with gen_random_uuid()
- Timestamp tracking for creation and expiration

**Storage Strategy:**
- Uploaded files stored in `/uploads` directory
- Unique filenames: `{timestamp}-{random}-{originalname}`
- In-memory storage adapter (MemStorage) as fallback for development
- Archiver library for ZIP creation on-demand

### Security Mechanisms

**Authentication & Authorization:**
- 6-digit numeric codes (100000-999999 range) with uniqueness validation
- Optional bcrypt password hashing for transfer protection
- Password verification before file access

**File Handling Security:**
- File size limits enforced at upload
- Filename sanitization via timestamp and random prefix
- MIME type validation and storage
- Total transfer size tracking

**Rate Limiting & Expiration:**
- Max download count enforcement per transfer
- Time-based expiration (configurable: minutes/hours/days)
- Automatic cleanup job for expired transfers (via getExpiredTransfers query)

### External Dependencies

**Core Libraries:**
- `express` - Web server framework
- `drizzle-orm` & `drizzle-kit` - Database ORM and migrations
- `@neondatabase/serverless` - PostgreSQL serverless driver
- `multer` - File upload middleware
- `archiver` - ZIP archive creation
- `bcrypt` - Password hashing
- `qrcode` - QR code generation

**Frontend Libraries:**
- `react` & `react-dom` - UI framework
- `@tanstack/react-query` - Server state management
- `wouter` - Lightweight routing
- `date-fns` - Date formatting
- `zod` - Runtime validation
- Radix UI components (@radix-ui/*) - Accessible primitives
- `tailwindcss` - Utility-first CSS
- `class-variance-authority` & `clsx` - Dynamic class composition

**Development Tools:**
- `vite` - Build tool and dev server
- `typescript` - Type safety
- `tsx` - TypeScript execution
- `esbuild` - Server bundle production build
- Replit-specific plugins for development experience

**Database:**
- PostgreSQL (via Neon serverless)
- Connection via DATABASE_URL environment variable
- Drizzle migrations in `/migrations` directory