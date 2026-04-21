# Smart Agri Platform - Technical Architecture

## Overview
E-commerce platform for agricultural products (similar to TikTok Shop) where users can:
- Post buy/sell listings
- Upload images and videos
- Create shop information
- Manage owned fields

## Tech Stack

### Core Framework
- **Frontend/Backend**: Next.js 14+ (App Router) - Monolith, easy to scale to microservices
- **Database**: PostgreSQL - Relational data (users, shops, products, fields)
- **ORM**: Prisma - Type-safe, migration support, easy maintenance
- **Storage**: MinIO or S3 (self-hosted) for images/videos
- **Container**: Docker - Standardized deployment

### Architecture Phases

#### Phase 1: Initial MVP (Monolith)
- Single Next.js project with:
  - `/api/*` - Backend API routes
  - `/app/*` - Frontend pages
  - Prisma schema defining models (User, Shop, Product, Field)

#### Phase 2: Scalability (Microservices Ready)
- Split `/api` into separate microservices (NestJS/Express)
- Add Redis for caching
- Add message queue (RabbitMQ/Kafka) for async tasks
- CDN for static assets

### Project Structure
```
/
├── prisma/           # Schema, migrations
├── app/              # Next.js App Router
├── lib/              # Services, utilities
├── components/       # Reusable UI components
├── public/uploads/   # Temporary storage (or external)
├── docker-compose.yml
└── .env.example
```

### Key Features to Implement
1. **User Management** - Registration, authentication, profiles
2. **Shop Management** - Create, update shops
3. **Product Listings** - Create, edit, delete products with media
4. **Field Management** - Register and manage agricultural fields
5. **Media Upload** - Image and video upload to storage
6. **Search & Discovery** - Browse products, shops

### Database Schema (Initial)
- Users (id, email, password, name, phone)
- Shops (id, userId, name, description, location)
- Products (id, shopId, name, description, price, images, videos)
- Fields (id, userId, name, location, area, cropType)

## Implementation Roadmap

### Phase 1: Foundation Setup

#### ✅ Completed Tasks
1. **[DONE] Initialize Next.js project with TypeScript**
   - Setup Next.js 14.2.18 with React 18
   - Configure TypeScript and Tailwind CSS
   - Create basic project structure (app/, components/, lib/, public/uploads/)
   - Add .gitignore and basic configuration files
   - Create initial home page and layout
   - Successfully build and test the project

#### 🔄 Pending Tasks
2. **[PENDING] Setup PostgreSQL and Prisma ORM**
   - Install Prisma CLI and client
   - Configure PostgreSQL database connection
   - Create database schema with models:
     - User (id, email, password, name, phone)
     - Shop (id, userId, name, description, location)
     - Product (id, shopId, name, description, price, images, videos)
     - Field (id, userId, name, location, area, cropType)
   - Generate and run initial migration
   - Setup Prisma client in lib/

3. **[PENDING] Setup Docker environment**
   - Create docker-compose.yml with services:
     - PostgreSQL database
     - MinIO for object storage (S3-compatible)
   - Configure environment variables (.env.example)
   - Setup volume persistence for data
   - Create development and production configurations

4. **[PENDING] Create authentication system**
   - Implement JWT or session-based authentication
   - Create API routes:
     - POST /api/auth/register
     - POST /api/auth/login
     - GET /api/auth/me
     - POST /api/auth/logout
   - Setup password hashing (bcrypt)
   - Create middleware for protected routes
   - Add user profile management

5. **[PENDING] Setup media upload with storage**
   - Configure MinIO/S3 connection
   - Create upload API endpoint (/api/upload)
   - Implement file validation (type, size limits)
   - Handle image and video uploads
   - Generate unique filenames
   - Create utility functions for file URLs

### Phase 2: Core Features (Not Started)
6. **[TODO] Shop Management**
7. **[TODO] Product Listings**
8. **[TODO] Field Management**
9. **[TODO] Search & Discovery**
10. **[TODO] Frontend UI Development**
