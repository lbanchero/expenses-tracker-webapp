# Deployment Guide for Expense Tracker PWA

## Prerequisites

1. **Supabase Project Setup** (Follow SUPABASE_SETUP.md)
2. **Digital Ocean Account** with Apps Platform access
3. **GitHub Repository** with your code

## Step 1: Prepare Your Environment

### 1.1 Update Supabase Credentials
In `index.html`, replace the placeholder values:
```javascript
const SUPABASE_URL = 'https://your-project.supabase.co';
const SUPABASE_ANON_KEY = 'your-anon-key-here';
```

### 1.2 Generate PWA Icons
1. Open `icon-generator.html` in your browser
2. Right-click each canvas and save as:
   - `icons/icon-192.png`
   - `icons/icon-512.png`

## Step 2: Digital Ocean Apps Deployment

### 2.1 Via GitHub Integration
1. Go to [Digital Ocean Apps](https://cloud.digitalocean.com/apps)
2. Click "Create App"
3. Choose "GitHub" as source
4. Select your repository: `lbanchero/expenses-tracker-webapp`
5. Choose branch: `main`

### 2.2 Configure App Settings
1. **App Name**: `expense-tracker-webapp`
2. **Plan**: Basic ($5/month) or Static Sites (Free)
3. **Build Settings**:
   - Build Command: `echo "No build needed"`
   - Output Directory: `/`

### 2.3 Environment Variables
Add these environment variables in the Digital Ocean Apps dashboard:
- `SUPABASE_URL`: Your Supabase project URL
- `SUPABASE_ANON_KEY`: Your Supabase anon key

### 2.4 Domain Configuration
1. Your app will be available at: `https://your-app-name.ondigitalocean.app`
2. For custom domain, add it in the "Domains" section

## Step 3: Update Supabase URLs

### 3.1 Authentication URLs
In your Supabase dashboard:
1. Go to Authentication > URL Configuration
2. Add your production URL:
   - Site URL: `https://your-app-name.ondigitalocean.app`
   - Redirect URLs: `https://your-app-name.ondigitalocean.app/**`

### 3.2 Google OAuth Configuration
Update your Google Cloud Console OAuth settings:
1. Add authorized redirect URI: `https://your-project.supabase.co/auth/v1/callback`
2. Add authorized JavaScript origins: `https://your-app-name.ondigitalocean.app`

## Step 4: Testing

### 4.1 PWA Installation
1. Visit your deployed app on mobile
2. Look for "Add to Home Screen" prompt
3. Test offline functionality by turning off network

### 4.2 Authentication Flow
1. Test Google sign-in
2. Verify user can add/edit/delete expenses
3. Check past months functionality

## Step 5: Performance Optimization

### 5.1 Enable HTTPS
- Digital Ocean Apps automatically provides HTTPS
- Verify your manifest.json works correctly

### 5.2 Service Worker
- Check browser dev tools > Application > Service Workers
- Verify caching is working properly

## Troubleshooting

### Common Issues

1. **Icons not loading**: Ensure icon files are in `/icons/` directory
2. **Supabase connection fails**: Check environment variables
3. **Google OAuth fails**: Verify redirect URLs in Google Console
4. **PWA not installable**: Check manifest.json and HTTPS

### Debug Steps

1. Open browser dev tools
2. Check Console for errors
3. Verify Network tab for failed requests
4. Check Application tab for PWA status

## Monitoring

### Digital Ocean Apps Dashboard
- Monitor app performance
- Check build logs
- View error logs

### Supabase Dashboard
- Monitor database usage
- Check authentication logs
- Review API usage

## Scaling Considerations

### Database
- Monitor Supabase usage limits
- Consider upgrading plan if needed

### App Performance
- Digital Ocean Apps auto-scales
- Monitor response times
- Consider CDN for global users

## Security

### Environment Variables
- Never commit secrets to Git
- Use Digital Ocean's environment variables
- Rotate keys regularly

### Supabase Security
- Row Level Security is enabled
- Users can only access their own data
- Regular security updates

## Backup Strategy

### Database Backups
- Supabase provides automatic backups
- Consider manual exports for critical data

### Code Backups
- GitHub repository serves as backup
- Tag releases for version control
