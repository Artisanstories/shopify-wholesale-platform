# Deployment Guide

## Quick Deploy to Production Platforms

### 1. Vercel (Recommended for Full-Stack)
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy to Vercel
vercel

# Add environment variables in Vercel dashboard
# - DATABASE_URL
# - SENDGRID_API_KEY (optional)
# - STRIPE_SECRET_KEY (optional)
# - VITE_STRIPE_PUBLIC_KEY (optional)
```

### 2. Railway
```bash
# Install Railway CLI
npm install -g @railway/cli

# Login and deploy
railway login
railway deploy

# Set environment variables
railway variables set DATABASE_URL=your_database_url
```

### 3. Render
1. Connect GitHub repository to Render
2. Create new Web Service
3. Build Command: `npm install && npm run build`
4. Start Command: `npm start`
5. Add environment variables in dashboard

### 4. Heroku
```bash
# Install Heroku CLI and login
heroku create your-app-name

# Add PostgreSQL addon
heroku addons:create heroku-postgresql:essential-0

# Deploy
git push heroku main

# Set environment variables
heroku config:set SENDGRID_API_KEY=your_key
```

### 5. DigitalOcean App Platform
1. Connect GitHub repository
2. Configure build settings:
   - Build Command: `npm run build`
   - Run Command: `npm start`
3. Add environment variables
4. Deploy

## Database Setup

### PostgreSQL (Required)
The application requires PostgreSQL. Choose one:

#### Option A: Neon (Recommended)
1. Sign up at [neon.tech](https://neon.tech)
2. Create new project
3. Copy connection string to `DATABASE_URL`

#### Option B: Supabase
1. Sign up at [supabase.com](https://supabase.com)
2. Create new project
3. Get connection string from Settings → Database

#### Option C: AWS RDS
1. Create PostgreSQL instance in AWS RDS
2. Configure security groups
3. Use connection details for `DATABASE_URL`

## Environment Configuration

### Required Variables
```env
DATABASE_URL=postgresql://user:password@host:port/database
```

### Optional Variables
```env
# Email notifications
SENDGRID_API_KEY=SG.your_sendgrid_api_key

# Payment processing
STRIPE_SECRET_KEY=sk_live_your_stripe_secret
VITE_STRIPE_PUBLIC_KEY=pk_live_your_stripe_public

# Production settings
NODE_ENV=production
PORT=3000
```

## Post-Deployment Setup

### 1. Initialize Database
After deployment, run database migrations:
```bash
npm run db:push
```

### 2. Verify API Endpoints
Test these endpoints:
- `GET /api/dashboard/metrics`
- `GET /api/applications`
- `POST /api/applications` (with test data)

### 3. Configure Custom Domain
Most platforms support custom domains:
- Vercel: Add domain in project settings
- Railway: Configure custom domain
- Render: Add custom domain in dashboard

### 4. SSL Certificate
All recommended platforms provide automatic SSL certificates.

## Monitoring & Maintenance

### Health Checks
Monitor these endpoints:
- `/api/dashboard/metrics` - Application health
- Database connectivity
- Email service status (if configured)

### Logging
Enable application logging in production:
```env
NODE_ENV=production
DEBUG=false
LOG_LEVEL=info
```

### Backup Strategy
- Database: Automated backups via hosting provider
- Application data: Regular exports via admin dashboard
- Configuration: Version control in GitHub

## Scaling Considerations

### Performance
- Database connection pooling (already configured)
- CDN for static assets
- Horizontal scaling for high traffic

### Security
- HTTPS enforced (handled by platform)
- Environment variables secured
- Database access restricted

### Updates
1. Commit changes to GitHub
2. Platform auto-deploys from main branch
3. Run database migrations if schema changed
4. Monitor deployment logs

This deployment guide covers the most popular platforms for hosting Node.js applications. Choose the platform that best fits your needs and budget.