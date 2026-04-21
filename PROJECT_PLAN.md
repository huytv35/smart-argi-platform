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
1. Project initialization with Next.js + Prisma
2. Database setup and schema definition
3. Authentication system
4. Basic CRUD for users, shops, products, fields
5. Media upload implementation
6. Frontend UI development
