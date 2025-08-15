# Shopify Wholesale Management Platform

A comprehensive enterprise-grade wholesale management system for Shopify stores with advanced VAT handling, customer application processing, and dynamic pricing rules.

## Features

### Core Wholesale Management
- **Customer Application System**: Automated wholesale application form with customizable fields
- **Admin Approval Workflow**: Multi-step application review and approval process
- **Customer Tier Management**: Hierarchical customer classification with tier-based pricing
- **Order Management**: Complete wholesale order tracking and management

### Advanced VAT & Pricing
- **Dual VAT Display**: Show both VAT-inclusive and VAT-exclusive prices simultaneously
- **Dynamic VAT Calculation**: Automatic VAT calculation at checkout based on customer status
- **Regional VAT Configuration**: Support for multiple VAT rates and regional tax settings
- **VAT Exemption Handling**: Automatic VAT exemption for registered wholesale customers

### Pricing & Discounts
- **Rule-Based Pricing Engine**: Flexible discount rules by customer tags, collections, and product types
- **Percentage & Fixed Discounts**: Support for both percentage and fixed-amount discounts
- **Minimum Order Requirements**: Configurable minimum quantities and order values
- **Tiered Pricing**: Volume-based discount tiers for wholesale customers

### Analytics & Reporting
- **Real-Time Dashboard**: Comprehensive metrics for revenue, applications, and customer activity
- **Customer Analytics**: Top customers by revenue and order frequency
- **Monthly Reporting**: Automated monthly metrics and trend analysis
- **Application Tracking**: Monitor application status and conversion rates

## Technology Stack

### Frontend
- **React 18** with TypeScript
- **Vite** for development and building
- **Tailwind CSS** with Shadcn/ui components
- **TanStack Query** for state management
- **Wouter** for routing
- **React Hook Form** with Zod validation

### Backend
- **Node.js** with Express.js
- **TypeScript** with ES modules
- **Drizzle ORM** for database operations
- **PostgreSQL** (Neon serverless)
- **Session-based authentication**

## Installation

### Prerequisites
- Node.js 18+ 
- PostgreSQL database
- Replit account (for deployment)

### Environment Variables
Create a `.env` file with the following variables:

```env
# Database
DATABASE_URL=your_postgresql_connection_string
PGHOST=your_pg_host
PGPORT=5432
PGUSER=your_pg_user
PGPASSWORD=your_pg_password
PGDATABASE=your_pg_database

# Optional: Email & Payment Processing
SENDGRID_API_KEY=your_sendgrid_key
STRIPE_SECRET_KEY=sk_your_stripe_secret
VITE_STRIPE_PUBLIC_KEY=pk_your_stripe_public
```

### Setup Steps

1. **Clone and Install Dependencies**
   ```bash
   git clone your-repository-url
   cd shopify-wholesale-platform
   npm install
   ```

2. **Database Setup**
   ```bash
   npm run db:push
   ```

3. **Start Development Server**
   ```bash
   npm run dev
   ```

4. **Access the Application**
   - Admin Dashboard: `http://localhost:5000/dashboard`
   - Customer Application Form: `http://localhost:5000/`

## Usage Guide

### Admin Dashboard
Access comprehensive wholesale management through the admin interface:

1. **Dashboard Overview**: View key metrics including total revenue, active customers, and pending applications
2. **Applications Management**: Review and approve/reject wholesale applications
3. **Customer Management**: Manage wholesale customers and their tier assignments
4. **Pricing Rules**: Create and manage discount rules and pricing configurations
5. **VAT Configuration**: Set up regional VAT rates and tax settings

### Customer Application Process
Customers can apply for wholesale access through a comprehensive form including:

- Business information and registration details
- VAT registration number (for tax exemption)
- Expected order volumes
- Business address and contact information

### Integration Features

#### VAT Handling
The platform provides sophisticated VAT management:
- Automatic detection of VAT-registered customers
- Dynamic price display (inclusive/exclusive)
- Checkout VAT calculation
- Regional VAT rate configuration

#### Pricing Engine
Flexible pricing rules support:
- Customer tag-based discounts
- Collection-specific pricing
- Product type discounts
- Minimum order requirements
- Tiered volume pricing

## API Endpoints

### Applications
- `GET /api/applications` - List all applications
- `POST /api/applications` - Submit new application
- `PATCH /api/applications/:id` - Update application status

### Customers
- `GET /api/customers` - List wholesale customers
- `POST /api/customers` - Create new customer
- `GET /api/customers/top/revenue` - Top customers by revenue

### Pricing Rules
- `GET /api/pricing-rules` - List pricing rules
- `POST /api/pricing-rules` - Create pricing rule
- `PUT /api/pricing-rules/:id` - Update pricing rule
- `DELETE /api/pricing-rules/:id` - Delete pricing rule

### VAT Configuration
- `GET /api/vat-config` - Get VAT settings
- `POST /api/vat-config` - Create/update VAT configuration

### Analytics
- `GET /api/dashboard/metrics` - Dashboard metrics
- `GET /api/monthly-metrics` - Monthly analytics

## Deployment

### Replit Deployment
1. Import project to Replit
2. Set environment variables in Replit Secrets
3. Run `npm install` 
4. Execute `npm run db:push`
5. Start with `npm run dev`
6. Deploy using Replit's deployment feature

### Manual Deployment
1. Build the application: `npm run build`
2. Set up production database
3. Configure environment variables
4. Run database migrations: `npm run db:push`
5. Start production server: `npm start`

## Configuration

### VAT Settings
Configure VAT handling through the admin interface:
- Set default VAT rate for your region
- Configure VAT-inclusive/exclusive display preferences
- Set up customer VAT exemption rules

### Pricing Rules
Create sophisticated pricing logic:
- Define customer tiers and associated discounts
- Set minimum order requirements
- Configure collection-specific pricing
- Implement volume-based discount tiers

### Email Notifications
Configure SendGrid for automated communications:
- Application confirmation emails
- Approval/rejection notifications
- Customer onboarding messages

## Development

### Database Schema
The application uses a comprehensive schema including:
- Users (admin authentication)
- Wholesale Applications (customer applications)
- Wholesale Customers (approved customers)
- VAT Configuration (tax settings)
- Pricing Rules (discount logic)
- Wholesale Orders (order management)
- Monthly Metrics (analytics)

### Adding New Features
1. Update database schema in `shared/schema.ts`
2. Run `npm run db:push` to apply changes
3. Update storage interface in `server/storage.ts`
4. Add API routes in `server/routes.ts`
5. Create frontend components and pages

## Support

For technical support or feature requests, please:
1. Check existing documentation
2. Review error logs in the admin dashboard
3. Ensure all required environment variables are set
4. Verify database connectivity

## License

This project is proprietary software designed for wholesale management applications.