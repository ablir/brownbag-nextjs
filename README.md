# Brownbag Next.js Monorepo

A modern full-stack monorepo application with Next.js 15 frontend and Express backend, featuring NextAuth.js v5 for authentication.

## Quick Start

### Prerequisites
- Node.js 18+
- npm
- Nginx (optional, for production-like setup)

### Installation & Running

```bash
# Clone the repository
git clone https://github.com/ablir/brownbag-nextjs.git
cd brownbag-nextjs

# Start all services (installs dependencies automatically)
./start.sh

# Stop all services
./stop.sh
```

The application will be available at:
- **Main app (via nginx)**: http://localhost:9898
- **Frontend (direct)**: http://localhost:3000
- **Backend API**: http://localhost:3001

## Features

- ✨ **Next.js 15** with App Router and Server Components
- 🔐 **NextAuth.js v5** (Auth.js) with credentials provider
- 🎨 **Tailwind CSS** for styling
- 🔄 **Express Backend** with TypeScript
- 🎭 **Mock Authentication** - accepts any credentials
- 👤 **User Profile** with fake data generation
- 🔄 **Nginx Reverse Proxy** for unified API access
- 📦 **Monorepo Structure** for easy management

## Tech Stack

### Frontend
- Next.js 15 (App Router)
- TypeScript
- NextAuth.js v5 (Auth.js)
- Tailwind CSS
- React 19

### Backend
- Express 5
- TypeScript
- Faker.js for mock data
- CORS enabled

### Infrastructure
- Nginx reverse proxy
- Bash scripts for easy startup/shutdown

## Project Structure

```
brownbag-nextjs/
├── frontend/               # Next.js application
│   ├── app/               # App Router pages
│   │   ├── api/auth/      # NextAuth API routes
│   │   ├── login/         # Login page
│   │   └── dashboard/     # User dashboard
│   ├── auth.ts            # NextAuth configuration
│   ├── middleware.ts      # Auth middleware
│   └── package.json
├── backend/               # Express backend
│   ├── src/
│   │   └── index.ts       # Main server file
│   └── package.json
├── nginx/                 # Nginx configuration
│   └── nginx.conf
├── start.sh              # Start all services
└── stop.sh               # Stop all services
```

## Authentication

This project uses **NextAuth.js v5** (also known as Auth.js), the latest version with enhanced features:

- Server-side authentication with App Router support
- JWT-based sessions
- Protected routes via middleware
- Credentials provider (accepts any username/password for demo)

### Login
- Navigate to `/login` or root URL
- Enter any username and password
- Redirects to dashboard after successful login

### Protected Routes
- All routes except `/login` require authentication
- Middleware handles automatic redirects
- Session managed via JWT tokens

## API Endpoints

### POST /api/login
Login endpoint that accepts any credentials (mock auth).

**Request:**
```json
{
  "username": "string",
  "password": "string"
}
```

**Response:**
```json
{
  "success": true,
  "message": "Login successful",
  "token": "jwt-token",
  "username": "string"
}
```

### GET /api/user/info
Get user information with fake data.

**Query Parameters:**
- `username`: User's username

**Response:**
```json
{
  "id": "uuid",
  "username": "string",
  "email": "email@example.com",
  "firstName": "string",
  "lastName": "string",
  "avatar": "url",
  "phone": "string",
  "address": { ... },
  "company": "string",
  "jobTitle": "string",
  "bio": "string",
  "joinedDate": "date",
  "lastLogin": "date"
}
```

## Development

### Running Services Separately

**Backend:**
```bash
cd backend
npm install
npm run dev
# Runs on http://localhost:3001
```

**Frontend:**
```bash
cd frontend
npm install
npm run dev
# Runs on http://localhost:3000
```

**Nginx (optional):**
```bash
nginx -c $(pwd)/nginx/nginx.conf -p $(pwd)/nginx/
# Runs on http://localhost:9898
```

### Environment Variables

**Frontend (.env.local):**
```env
AUTH_SECRET=your-secret-key-change-this-in-production
NEXTAUTH_URL=http://localhost:3000
NEXT_PUBLIC_API_URL=http://localhost:3001
```

**Backend (.env):**
```env
PORT=3001
NODE_ENV=development
```

## Modern Next.js Features

This project showcases modern Next.js 15 patterns:

1. **App Router** - Using the new app directory structure
2. **Server Components** - Default server-side rendering
3. **Server Actions** - For form submissions and mutations
4. **Middleware** - Route protection and redirects
5. **NextAuth.js v5** - Latest authentication patterns
6. **Tailwind CSS** - Utility-first styling
7. **TypeScript** - Full type safety

## Scripts

- `./start.sh` - Start all services (backend, frontend, nginx)
- `./stop.sh` - Stop all running services
- `npm run dev` - Run frontend/backend in development mode
- `npm run build` - Build for production
- `npm run lint` - Run ESLint

## License

ISC
