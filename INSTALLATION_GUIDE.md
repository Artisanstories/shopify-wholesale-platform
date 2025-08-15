# Installation Guide: Shopify Wholesale Platform

## Overview
This guide will help you install and configure the Shopify wholesale management platform to enable wholesale pricing, customer applications, and VAT handling for your business.

## Quick Start (5 Minutes)

### Step 1: Environment Setup
1. **Fork this repository** to your GitHub account
2. **Create a Replit account** if you don't have one
3. **Import the project** to Replit from your GitHub fork

### Step 2: Database Configuration
1. In your Replit project, the PostgreSQL database is automatically provisioned
2. Run the database setup:
   ```bash
   npm install
   npm run db:push
   ```

### Step 3: Start the Application
1. Click the "Run" button in Replit or execute:
   ```bash
   npm run dev
   ```
2. Your application will be available at your Replit URL

## Detailed Configuration

### Required Environment Variables
The following are automatically configured in Replit:
- `DATABASE_URL` - PostgreSQL connection string
- `PGHOST`, `PGPORT`, `PGUSER`, `PGPASSWORD`, `PGDATABASE` - Database connection details

### Optional Environment Variables (for enhanced features)
Add these in Replit Secrets if you want email notifications and payment processing:

```
SENDGRID_API_KEY=your_sendgrid_api_key
STRIPE_SECRET_KEY=sk_your_stripe_secret_key
VITE_STRIPE_PUBLIC_KEY=pk_your_stripe_publishable_key
```

## Shopify Integration Options

### Option 1: Standalone Wholesale Portal (Recommended)
Host the platform independently and direct wholesale customers to your Replit URL:
- Share your Replit app URL with potential wholesale customers
- Customers complete applications through your platform
- Manage all wholesale operations through the admin dashboard

### Option 2: Embedded Application Form
Embed the wholesale application form into your existing website:

1. **Get the embed code** from your running application at `/embed-code`
2. **Add the code** to your website where you want the application form
3. **Style the form** to match your website design

```html
<!-- Example embed code -->
<iframe 
  src="https://your-replit-url.repl.co/"
  width="100%" 
  height="800px" 
  frameborder="0">
</iframe>
```

### Option 3: API Integration
Use the REST API to integrate with your existing systems:

```javascript
// Example: Submit wholesale application
const response = await fetch('https://your-replit-url.repl.co/api/applications', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    businessName: 'Customer Business',
    contactName: 'John Doe',
    email: 'john@business.com',
    phoneNumber: '+44 20 1234 5678',
    // ... other fields
  })
});
```

## Platform Features Overview

### Customer Application System
- **Professional Application Form**: Comprehensive form with business validation
- **Automated Processing**: Email notifications and status tracking
- **Document Upload**: Support for business registration documents
- **VAT Registration**: Automatic VAT exemption handling

### Admin Management
Access the admin dashboard at `https://your-replit-url.repl.co/dashboard`:

1. **Applications Review**: Approve or reject wholesale applications
2. **Customer Management**: Manage wholesale customer accounts and tiers
3. **Pricing Configuration**: Set up discount rules and pricing tiers
4. **VAT Settings**: Configure regional VAT rates and exemptions
5. **Analytics Dashboard**: Monitor revenue, applications, and performance

### Pricing & VAT Features

#### Dual VAT Display
Show both VAT-inclusive and VAT-exclusive prices:
```javascript
import { calculateVATExclusive, calculateVATInclusive } from './lib/vat-utils';

const priceIncVAT = calculateVATInclusive(100, 20); // £120.00
const priceExVAT = calculateVATExclusive(120, 20);  // £100.00
```

#### Customer-Specific Pricing
Apply discounts based on:
- Customer tier (Bronze, Silver, Gold, Platinum)
- Order volume
- Product collections
- Customer tags

## Customization Guide

### Branding & Styling
1. **Update Colors**: Edit `client/src/index.css` to match your brand colors
2. **Logo Replacement**: Replace logo files in the assets directory
3. **Custom Styling**: Modify Tailwind classes in component files

### Application Form Fields
Add custom fields to the wholesale application:

1. **Update Schema**: Edit `shared/schema.ts` to add new fields
2. **Update Form**: Modify `client/src/components/forms/wholesale-application-form.tsx`
3. **Database Migration**: Run `npm run db:push`

Example - Adding "Industry" field:
```typescript
// In shared/schema.ts
export const wholesaleApplications = pgTable('wholesale_applications', {
  // ... existing fields
  industry: text('industry'),
});

// In the form component
<FormField
  control={form.control}
  name="industry"
  render={({ field }) => (
    <FormItem>
      <FormLabel>Industry</FormLabel>
      <FormControl>
        <Input placeholder="e.g., Retail, Manufacturing" {...field} />
      </FormControl>
      <FormMessage />
    </FormItem>
  )}
/>
```

### Email Notifications (Optional)
Configure SendGrid for automated emails:

1. **Create SendGrid Account**: Sign up at sendgrid.com
2. **Get API Key**: Generate API key in SendGrid dashboard
3. **Add to Secrets**: Add `SENDGRID_API_KEY` in Replit Secrets
4. **Configure Templates**: Customize email templates in the admin dashboard

### Payment Integration (Optional)
Set up Stripe for payment processing:

1. **Create Stripe Account**: Sign up at stripe.com
2. **Get API Keys**: 
   - `STRIPE_SECRET_KEY` (starts with `sk_`)
   - `VITE_STRIPE_PUBLIC_KEY` (starts with `pk_`)
3. **Add to Secrets**: Add both keys in Replit Secrets
4. **Test Payments**: Use Stripe test mode for development

## Production Deployment

### Replit Deployment (Recommended)
1. **Enable Always On**: Keep your application running 24/7
2. **Custom Domain**: Connect your custom domain in Replit settings
3. **Environment Variables**: Ensure all secrets are properly configured
4. **Database Backup**: Set up automated database backups

### Alternative Hosting
The platform can be deployed to any Node.js hosting provider:

1. **Vercel/Netlify**: For frontend deployment
2. **Heroku/Railway**: For full-stack deployment
3. **AWS/Google Cloud**: For enterprise hosting
4. **Self-hosted**: On your own servers

## Security Considerations

### Data Protection
- All customer data is encrypted in transit and at rest
- VAT registration numbers are securely stored
- Business information is protected with appropriate access controls

### Access Control
- Admin dashboard requires authentication
- Customer applications are rate-limited
- Database access is restricted to authorized connections

### Compliance
- GDPR compliance for EU customers
- VAT calculation accuracy for tax compliance
- Business data retention policies

## Support & Maintenance

### Monitoring
- Application error tracking
- Database performance monitoring
- Customer application analytics

### Updates
1. **Pull latest changes** from the repository
2. **Run database migrations**: `npm run db:push`
3. **Test functionality** in development
4. **Deploy updates** to production

### Troubleshooting

#### Common Issues:
1. **Database Connection**: Check `DATABASE_URL` in environment variables
2. **Form Submissions**: Verify API endpoints are accessible
3. **Email Notifications**: Confirm SendGrid API key is valid
4. **Payment Processing**: Check Stripe configuration

#### Debug Mode:
Enable detailed logging by adding:
```
DEBUG=true
```
to your environment variables.

## Getting Help

### Documentation
- Review the complete README.md for detailed feature information
- Check API documentation for integration details
- Review database schema for data structure

### Technical Support
1. Check error logs in the admin dashboard
2. Review browser console for frontend issues
3. Verify environment variable configuration
4. Test database connectivity

This platform provides enterprise-grade wholesale management with minimal setup time. Follow this guide to have your wholesale portal operational within minutes.