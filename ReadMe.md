# Backend API Development Guide

## 🎯 Overview

Welcome! You're responsible for building the backend API for our multi-platform e-commerce application. The frontend (Next.js web + Expo mobile) is already set up and ready to consume your API endpoints.

---

## 📁 Your Workspace

```
ecommerce-platform/
└── apps/
    └── api/          👈 THIS IS YOUR FOLDER - Work here only
```

**Important:** You have complete freedom in this folder. Choose any language/framework you prefer!

---

## 🛠️ Technology Options

You can build the API using **any** of these technologies:

### Option 1: Node.js + Express (Recommended)
- **Why:** Most common, large ecosystem, easy to integrate
- **Database Options:** PostgreSQL, MongoDB, MySQL
- **ORM Options:** TypeORM, Prisma, Mongoose

### Option 2: Python + FastAPI
- **Why:** Fast, modern, automatic API docs, great for ML integration
- **Database Options:** PostgreSQL, MongoDB, MySQL
- **ORM Options:** SQLAlchemy, Tortoise ORM

### Option 3: Python + Django REST Framework
- **Why:** Batteries included, admin panel out of the box
- **Database:** PostgreSQL, MySQL
- **ORM:** Django ORM (built-in)

### Option 4: Go + Gin/Fiber
- **Why:** High performance, compiled, great for scale
- **Database:** PostgreSQL, MongoDB
- **ORM:** GORM

### Option 5: PHP + Laravel
- **Why:** Mature ecosystem, rapid development
- **Database:** MySQL, PostgreSQL
- **ORM:** Eloquent (built-in)

### Option 6: Java + Spring Boot
- **Why:** Enterprise-ready, robust, scalable
- **Database:** PostgreSQL, MySQL, MongoDB
- **ORM:** JPA/Hibernate

---

## 🚀 Getting Started

### Step 1: Navigate to Your Workspace

```bash
cd apps/api
```

### Step 2: Choose Your Stack

Pick one from the options above and initialize your project.

---

## 📦 Setup Examples for Each Stack

### For Node.js + Express

```bash
cd apps/api

# Initialize project
npm init -y

# Install core dependencies
npm install express cors dotenv

# For PostgreSQL
npm install pg typeorm reflect-metadata
# OR for MongoDB
npm install mongoose

# Install auth & security
npm install bcryptjs jsonwebtoken express-validator

# Install utilities
npm install multer aws-sdk stripe nodemailer

# Install dev dependencies
npm install -D typescript @types/express @types/node @types/cors @types/bcryptjs @types/jsonwebtoken ts-node-dev nodemon

# Initialize TypeScript (optional but recommended)
npx tsc --init

# Create basic structure
mkdir -p src/{config,models,controllers,routes,middleware,services,utils}

# Create entry file
touch src/server.ts
```

**Run Command:**
```bash
# Development
npm run dev

# Production
npm start
```

---

### For Python + FastAPI

```bash
cd apps/api

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install fastapi uvicorn[standard] python-dotenv

# For PostgreSQL
pip install sqlalchemy psycopg2-binary alembic
# OR for MongoDB
pip install motor pymongo

# Install auth & utilities
pip install python-jose[cryptography] passlib[bcrypt] python-multipart
pip install boto3 stripe python-decouple

# Create structure
mkdir -p app/{models,routes,services,utils,config}
touch app/main.py app/__init__.py

# Create requirements.txt
pip freeze > requirements.txt
```

**Run Command:**
```bash
# Development
uvicorn app.main:app --reload --port 5000

# Production
uvicorn app.main:app --host 0.0.0.0 --port 5000
```

---

### For Python + Django

```bash
cd apps/api

# Create virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Install Django and DRF
pip install django djangorestframework django-cors-headers python-dotenv

# For PostgreSQL
pip install psycopg2-binary

# Additional packages
pip install djangorestframework-simplejwt pillow boto3 stripe

# Create Django project
django-admin startproject core .

# Create apps
python manage.py startapp users
python manage.py startapp products
python manage.py startapp orders
python manage.py startapp sellers

# Create requirements.txt
pip freeze > requirements.txt
```

**Run Command:**
```bash
# Run migrations
python manage.py makemigrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Development
python manage.py runserver 0.0.0.0:5000

# Production (use gunicorn)
pip install gunicorn
gunicorn core.wsgi:application --bind 0.0.0.0:5000
```

---

### For Go + Gin

```bash
cd apps/api

# Initialize Go module
go mod init ecommerce-api

# Install dependencies
go get -u github.com/gin-gonic/gin
go get -u github.com/gin-contrib/cors
go get -u gorm.io/gorm
go get -u gorm.io/driver/postgres  # or driver/mysql
go get -u github.com/golang-jwt/jwt/v5
go get -u golang.org/x/crypto/bcrypt
go get -u github.com/joho/godotenv

# Create structure
mkdir -p {config,models,controllers,routes,middleware,services,utils}
touch main.go
```

**Run Command:**
```bash
# Development
go run main.go

# Build for production
go build -o server
./server
```

---

### For PHP + Laravel

```bash
cd apps/api

# Install Laravel (requires Composer)
composer create-project laravel/laravel .

# Install packages
composer require laravel/sanctum
composer require stripe/stripe-php
composer require aws/aws-sdk-php

# Set up database
php artisan migrate

# Install Laravel Passport for API auth (optional)
composer require laravel/passport
php artisan passport:install
```

**Run Command:**
```bash
# Development
php artisan serve --host=0.0.0.0 --port=5000

# Production (use with Nginx/Apache)
```

---

### For Java + Spring Boot

```bash
cd apps/api

# Use Spring Initializr (https://start.spring.io/) or
# Create manually with Maven/Gradle

# With Maven, your pom.xml should include:
# - Spring Web
# - Spring Data JPA
# - Spring Security
# - PostgreSQL Driver (or your choice)
# - Lombok

# Create structure
mkdir -p src/main/java/com/ecommerce/{config,models,controllers,services,repositories,security}
```

**Run Command:**
```bash
# Development with Maven
./mvnw spring-boot:run

# Development with Gradle
./gradlew bootRun

# Production
./mvnw clean package
java -jar target/ecommerce-api.jar
```

---

## 🔌 API Requirements

### Base URL
Your API should run on: `http://localhost:5000/api/v1`

### Required Endpoints

Refer to the **API Structure document** for complete endpoint specifications. Here's a summary:

#### Authentication
- `POST /api/v1/auth/register`
- `POST /api/v1/auth/login`
- `POST /api/v1/auth/refresh`
- `POST /api/v1/auth/logout`

#### Products
- `GET /api/v1/products` (public)
- `GET /api/v1/products/:id` (public)
- `POST /api/v1/seller/products` (auth required)
- `PUT /api/v1/seller/products/:id` (auth required)

#### Orders
- `POST /api/v1/orders` (auth required)
- `GET /api/v1/orders` (auth required)
- `GET /api/v1/orders/:id` (auth required)

#### Cart
- `GET /api/v1/cart` (auth required)
- `POST /api/v1/cart` (auth required)
- `DELETE /api/v1/cart/:itemId` (auth required)

### Response Format

**Success Response:**
```json
{
  "success": true,
  "data": {
    // your data here
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable message",
    "details": {}
  }
}
```

### CORS Configuration

Allow these origins:
- `http://localhost:3000` (Next.js web)
- `http://localhost:19006` (Expo web)
- `exp://` (Expo mobile - development)

---

## 🗄️ Database Setup

### PostgreSQL (Recommended)

```bash
# Install PostgreSQL (macOS)
brew install postgresql@15

# Start PostgreSQL
brew services start postgresql@15

# Create database
psql postgres
CREATE DATABASE ecommerce;
CREATE USER ecommerce_user WITH PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE ecommerce TO ecommerce_user;
\q
```

### MongoDB

```bash
# Install MongoDB (macOS)
brew tap mongodb/brew
brew install mongodb-community@7.0

# Start MongoDB
brew services start mongodb-community@7.0

# Create database (happens automatically on first connection)
mongosh
use ecommerce
```

### MySQL

```bash
# Install MySQL (macOS)
brew install mysql

# Start MySQL
brew services start mysql

# Create database
mysql -u root -p
CREATE DATABASE ecommerce;
CREATE USER 'ecommerce_user'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON ecommerce.* TO 'ecommerce_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

---

## 🔐 Environment Variables

Create a `.env` file in `apps/api/`:

```env
# Server
NODE_ENV=development
PORT=5000
API_VERSION=v1

# Database (PostgreSQL example)
DATABASE_URL=postgresql://ecommerce_user:your_password@localhost:5432/ecommerce

# OR MongoDB
# MONGODB_URI=mongodb://localhost:27017/ecommerce

# OR MySQL
# DATABASE_URL=mysql://ecommerce_user:your_password@localhost:3306/ecommerce

# JWT
JWT_SECRET=your-super-secret-jwt-key-change-this-in-production
JWT_EXPIRES_IN=24h
REFRESH_TOKEN_SECRET=your-refresh-token-secret-change-this-too
REFRESH_TOKEN_EXPIRES_IN=30d

# AWS S3 (for file uploads)
AWS_ACCESS_KEY_ID=your-aws-key
AWS_SECRET_ACCESS_KEY=your-aws-secret
AWS_REGION=us-east-1
AWS_S3_BUCKET=your-bucket-name

# Stripe (payment)
STRIPE_SECRET_KEY=sk_test_your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=whsec_your_webhook_secret

# Email (SendGrid example)
SENDGRID_API_KEY=your-sendgrid-api-key
FROM_EMAIL=noreply@yourstore.com

# Frontend URLs (for CORS)
FRONTEND_WEB_URL=http://localhost:3000
FRONTEND_MOBILE_URL=http://localhost:19006

# Redis (optional - for caching)
REDIS_URL=redis://localhost:6379
```

---

## 📝 Bash Scripts

Create these scripts in `apps/api/` folder:

### For Node.js - `dev.sh`
```bash
#!/bin/bash
echo "🚀 Starting API Server in Development Mode..."
npm run dev
```

### For Python - `dev.sh`
```bash
#!/bin/bash
echo "🚀 Starting API Server in Development Mode..."
source venv/bin/activate
uvicorn app.main:app --reload --port 5000
```

### For Django - `dev.sh`
```bash
#!/bin/bash
echo "🚀 Starting Django API Server..."
source venv/bin/activate
python manage.py runserver 0.0.0.0:5000
```

### For Go - `dev.sh`
```bash
#!/bin/bash
echo "🚀 Starting Go API Server..."
go run main.go
```

### Make scripts executable:
```bash
chmod +x dev.sh
```

### Run the script:
```bash
./dev.sh
```

---

## 🧪 Testing Your API

### Using cURL
```bash
# Test health endpoint
curl http://localhost:5000/api/v1/health

# Test registration
curl -X POST http://localhost:5000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","password":"password123","firstName":"John","lastName":"Doe"}'
```

### Using Postman/Insomnia
1. Import the API collection (create one based on endpoints)
2. Set base URL: `http://localhost:5000/api/v1`
3. Test each endpoint

---

## 📚 Reference Documents

In this project, you have access to:

1. **Database Schema** - Complete database design with all tables and relationships
2. **API Endpoints** - Full API specification with request/response formats
3. **Authentication Flow** - JWT implementation guide

Check the project documentation for these details.

---

## 🔄 Integration with Frontend

### CORS Setup (Node.js Example)

```javascript
const cors = require('cors');

app.use(cors({
  origin: [
    'http://localhost:3000',      // Next.js web
    'http://localhost:19006',     // Expo web
    /^exp:\/\/.*/                 // Expo mobile
  ],
  credentials: true
}));
```

### API Client Configuration

The frontend expects these headers in responses:
- `Content-Type: application/json`
- `Authorization: Bearer <token>` (for authenticated requests)

---

## 🐛 Troubleshooting

### Port Already in Use
```bash
# Find process using port 5000
lsof -i :5000

# Kill the process
kill -9 <PID>
```

### Database Connection Issues
- Check if database service is running
- Verify credentials in `.env`
- Check firewall settings

### CORS Errors
- Verify frontend URL in CORS configuration
- Check if credentials are enabled
- Ensure proper headers are set

---

## 📦 Deployment (When Ready)

### Recommended Platforms:
- **Railway** - Easy Node.js/Python deployment
- **Heroku** - Classic PaaS (free tier available)
- **DigitalOcean App Platform** - Good for all languages
- **AWS EC2** - Full control
- **Vercel** - Good for Node.js/serverless
- **Render** - Free tier, supports Docker

---

## 🤝 Communication with Frontend Team

### What Frontend Needs from You:
1. **API Base URL**: `http://localhost:5000/api/v1`
2. **Authentication Token Format**: `Bearer <token>`
3. **Response Format**: JSON with `success`, `data`, `error` structure
4. **Endpoint Documentation**: List of all available endpoints
5. **Error Codes**: Standard error codes and messages

### What You Need from Frontend:
- Nothing! They're ready and waiting for your API 😊

---

## ✅ Checklist

Before you start coding:
- [ ] Choose your technology stack
- [ ] Set up database (PostgreSQL/MongoDB/MySQL)
- [ ] Create `.env` file with all variables
- [ ] Install all dependencies
- [ ] Create basic project structure
- [ ] Test basic server is running on port 5000
- [ ] Implement health check endpoint: `GET /api/v1/health`
- [ ] Set up CORS for frontend URLs
- [ ] Implement authentication endpoints first
- [ ] Document your endpoints as you build

---

---

## 🚀 Running The Complete Application

Once you have your backend set up, you can run the entire application from the **root directory**:

```bash
# From the root: ecommerce-platform/

# Run Next.js Web App (Frontend)
npm run dev:web      # Runs on http://localhost:3000

# Run Expo Mobile App
npm run dev:mobile   # Runs on Expo Dev Server

# Run Backend API
npm run dev:api      # Runs on http://localhost:5000
```

### Run All Services Together

You can open **3 terminal windows** and run each service:

**Terminal 1 - Backend:**
```bash
cd ecommerce-platform
npm run dev:api
```

**Terminal 2 - Web Frontend:**
```bash
cd ecommerce-platform
npm run dev:web
```

**Terminal 3 - Mobile App:**
```bash
cd ecommerce-platform
npm run dev:mobile
```

### Quick Start Order

1. **Start Backend First** - `npm run dev:api` (Port 5000)
2. **Start Web App** - `npm run dev:web` (Port 3000)
3. **Start Mobile App** - `npm run dev:mobile` (Expo Dev Server)

---

## 🎉 You're Ready!

Choose your stack, set up your environment, and start building! The frontend is waiting for your amazing API.

**Questions?** Check the API documentation or reach out to the team.

Happy coding! 🚀