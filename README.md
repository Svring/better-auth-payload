# Better Auth + Payload CMS Template

A production-ready template combining [Payload CMS](https://payloadcms.com) and [Better Auth](https://www.better-auth.com) for building modern web applications with a powerful headless CMS and robust authentication system.

## Overview

This template provides a seamless integration between Payload CMS and Better Auth, allowing you to leverage Payload's content management capabilities alongside Better Auth's flexible authentication system. Built on Next.js 16 with TypeScript, PostgreSQL, and Bun runtime support.

## Features

- 🔐 **Better Auth Integration** - Modern authentication with email/password support
- 📦 **Payload CMS** - Headless CMS with admin dashboard
- 🎯 **Admin Access Control** - Role-based access control (RBAC) with admin/user permissions
- 🗄️ **PostgreSQL Database** - Using Drizzle ORM for type-safe database operations
- 🐰 **Bun Runtime** - Fast JavaScript runtime for development and production
- 🎨 **Modern UI** - Tailwind CSS with shadcn/ui components
- 🔍 **Developer Tools** - Ultracite for linting and Drizzle Studio for database management

## Enhancements Over Original

This repository is a fork of [ElysMaldov/payload-better_auth-example](https://github.com/ElysMaldov/payload-better_auth-example) with the following additions:

### Admin Plugin & Access Control

- **Better Auth Admin Plugin** - Integrated admin plugin for role-based access control
- **Permission System** - Configured admin and user roles with granular permissions
- **Protected Admin Routes** - Payload CMS admin dashboard protected by Better Auth permissions
- **Access Control** - Users collection configured to check admin permissions before allowing access

### Additional Tools & Packages

- **Ultracite** - Modern linting and code formatting tool (`lint:check`, `lint:fix`)
- **Drizzle Studio** - Visual database GUI for managing your PostgreSQL database (`drizzle:studio`)
- **Docker Support** - Optimized Dockerfile using Bun runtime for containerized deployments
- **Tailwind CSS v4** - Latest Tailwind CSS with PostCSS integration
- **Geist Font** - Modern typeface for improved typography

## Getting Started

### Prerequisites

- Node.js 18+ or Bun 1.0+
- PostgreSQL database
- Environment variables configured (see `.env.example`)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/your-username/better-auth-payload.git
cd better-auth-payload
```

2. Install dependencies:
```bash
bun install
# or
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your database URI and Payload secret
```

4. Generate Payload schema:
```bash
bun run payload:schema
```

5. Start the development server:
```bash
bun run dev
# or
npm run dev
```

### Available Scripts

- `dev` - Start development server
- `build` - Build for production
- `start` - Start production server
- `lint:check` - Check code with Ultracite
- `lint:fix` - Fix code issues with Ultracite
- `payload:schema` - Generate Payload database schema
- `drizzle:studio` - Open Drizzle Studio for database management
- `build:mac` - Build Docker image for macOS
- `build:linux` - Build Docker image for Linux/AMD64

## Project Structure

```
src/
├── app/                    # Next.js app router
│   ├── (frontend)/        # Public frontend routes
│   ├── (payload)/         # Payload CMS routes
│   └── api/               # API routes
├── auth/                   # Better Auth configuration
│   ├── auth.ts            # Main auth setup with admin plugin
│   ├── auth-client.ts     # Client-side auth utilities
│   └── permissions.ts     # Access control definitions
├── collections/            # Payload CMS collections
│   ├── auth/              # Auth-related collections
│   └── Media.ts           # Media collection
└── components/            # React components
```

## Admin Access Control

The admin plugin is configured in `src/auth/auth.ts` with the following setup:

- **Admin Role**: Full access to admin dashboard (`adminDashboard: ["read"]`)
- **User Role**: No admin access (`adminDashboard: []`)
- **Permission Checks**: Payload CMS collections check for admin permissions before allowing access

To grant a user admin access, ensure they have the `adminDashboard: ["read"]` permission in Better Auth.

## Database Management

### Drizzle Studio

Launch the visual database GUI:
```bash
bun run drizzle:studio
```

This opens a web interface at `http://localhost:4983` where you can:
- Browse tables and data
- Run queries
- Manage database schema
- View relationships

### Schema Generation

Generate Payload's database schema:
```bash
bun run payload:schema
```

This updates `src/payload-generated-schema.ts` based on your Payload collections.

## Docker Deployment

The project includes a Dockerfile optimized for Bun runtime:

```bash
# Build for your platform
bun run build:mac      # macOS
bun run build:linux    # Linux/AMD64

# Run the container
docker run -p 3000:3000 puddlecat/better-auth-payload:latest
```

The Dockerfile uses multi-stage builds for optimal image size and includes:
- Bun runtime for faster startup
- Standalone Next.js output
- Production optimizations

## Environment Variables

Required environment variables:

```env
DATABASE_URI=postgresql://user:password@localhost:5432/dbname
PAYLOAD_SECRET=your-secret-key-here
```

Optional:
```env
NODE_ENV=production
PORT=3000
```

## Credits

This project is based on the excellent work by [ElysMaldov](https://github.com/ElysMaldov) in the original [payload-better_auth-example](https://github.com/ElysMaldov/payload-better_auth-example) repository.

## License

MIT

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

