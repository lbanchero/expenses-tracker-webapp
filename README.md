# 💰 Expense Tracker PWA

A modern, mobile-first Progressive Web App for tracking personal expenses, built with React, Tailwind CSS, and Supabase.

## ✨ Features

- **🔐 Google OAuth Authentication** - Secure sign-in with Google
- **📱 Mobile-First Design** - Optimized for mobile devices with dark theme
- **💜 Modern UI** - Dark violet and green color scheme with smooth animations
- **📊 Monthly Overview** - View total EUR spent per month with visual summaries
- **📝 Quick Expense Entry** - Add expenses with minimal fields (amount, description, date)
- **📅 Historical Data** - View and manage expenses from past months
- **✏️ Edit & Delete** - Full CRUD operations for expense management
- **🔄 Offline Support** - Works offline with service worker caching
- **📲 PWA Installation** - Install as native app on mobile devices
- **🔒 Secure Data** - Row-level security with Supabase

## 🚀 Quick Start

### Prerequisites

- Supabase account
- Google Cloud Console account (for OAuth)
- Digital Ocean account (for deployment)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/lbanchero/expenses-tracker-webapp.git
   cd expenses-tracker-webapp
   ```

2. **Set up Supabase**
   - Follow the detailed guide in `SUPABASE_SETUP.md`
   - Create your Supabase project
   - Configure Google OAuth
   - Set up the database schema

3. **Configure the app**
   - Open `index.html`
   - Replace `YOUR_SUPABASE_URL` and `YOUR_SUPABASE_ANON_KEY` with your actual values

4. **Generate PWA icons**
   - Open `icon-generator.html` in your browser
   - Save the generated icons as `icons/icon-192.png` and `icons/icon-512.png`

5. **Test locally**
   - Open `index.html` in your browser
   - Or use a local server: `python -m http.server 8000`

## 🏗️ Architecture

### Tech Stack

- **Frontend**: React 18 (via CDN), Tailwind CSS
- **Backend**: Supabase (PostgreSQL, Auth, Real-time)
- **PWA**: Service Worker, Web App Manifest
- **Deployment**: Digital Ocean Apps Platform

### File Structure

```
expenses-tracker-webapp/
├── index.html              # Main application file
├── manifest.json           # PWA manifest
├── sw.js                   # Service worker
├── icon-generator.html     # Icon generation utility
├── icons/                  # PWA icons
│   ├── icon-192.png
│   └── icon-512.png
├── .do/
│   └── app.yaml           # Digital Ocean deployment config
├── SUPABASE_SETUP.md      # Supabase setup guide
├── DEPLOYMENT.md          # Deployment guide
└── README.md              # This file
```

### Database Schema

**transactions table:**
- `id` (UUID, primary key)
- `user_id` (UUID, foreign key to auth.users)
- `amount` (decimal, EUR amounts)
- `description` (text)
- `transaction_date` (date)
- `created_at` (timestamp)

## 🎨 Design System

### Colors
- **Primary**: Dark Violet (#8B5CF6)
- **Secondary**: Green (#10B981)
- **Background**: Dark Gray (#1F2937)
- **Cards**: Darker Gray (#111827)
- **Text**: Light Gray (#F9FAFB)

### Typography
- **Headers**: Semibold, responsive sizing
- **Body**: Regular weight, optimized for readability
- **Currency**: Bold, prominent display

### Components
- **Mobile-first responsive design**
- **Touch-friendly buttons (44px minimum)**
- **Smooth transitions and animations**
- **Loading states and error handling**

## 📱 PWA Features

### Installation
- Installable on iOS and Android
- Standalone app experience
- Custom splash screen
- App shortcuts for quick actions

### Offline Support
- Service worker caching
- Offline transaction viewing
- Background sync for pending data
- Graceful offline/online transitions

### Performance
- Fast loading with CDN resources
- Minimal bundle size
- Optimized images and assets
- Efficient data fetching

## 🔒 Security

### Authentication
- Google OAuth integration
- Secure session management
- Automatic token refresh

### Data Protection
- Row-Level Security (RLS) enabled
- Users can only access their own data
- Secure API endpoints
- Environment variable protection

## 🚀 Deployment

### Digital Ocean Apps
1. Follow the guide in `DEPLOYMENT.md`
2. Connect your GitHub repository
3. Configure environment variables
4. Deploy with zero-downtime updates

### Environment Variables
- `SUPABASE_URL`: Your Supabase project URL
- `SUPABASE_ANON_KEY`: Your Supabase anonymous key

## 🧪 Testing

### Manual Testing Checklist
- [ ] Google OAuth sign-in/sign-out
- [ ] Add new expense with validation
- [ ] Edit existing expense
- [ ] Delete expense with confirmation
- [ ] View current month summary
- [ ] Navigate to past months
- [ ] PWA installation prompt
- [ ] Offline functionality
- [ ] Mobile responsiveness

### Browser Support
- Chrome/Edge 88+
- Firefox 85+
- Safari 14+
- Mobile browsers with PWA support

## 🔧 Development

### Local Development
```bash
# Serve locally
python -m http.server 8000
# or
npx serve .
```

### Debugging
- Use browser dev tools
- Check Console for errors
- Monitor Network requests
- Verify Service Worker status
- Test PWA features in Application tab

## 📈 Performance

### Lighthouse Scores (Target)
- Performance: 90+
- Accessibility: 95+
- Best Practices: 90+
- SEO: 90+
- PWA: 100

### Optimization Features
- Efficient React rendering
- Optimized images
- Service worker caching
- Minimal external dependencies
- Fast CDN delivery

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

### Documentation
- `SUPABASE_SETUP.md` - Database and auth setup
- `DEPLOYMENT.md` - Deployment instructions

### Common Issues
- **PWA not installing**: Check HTTPS and manifest.json
- **Auth failing**: Verify Google OAuth configuration
- **Data not loading**: Check Supabase credentials and RLS policies

### Getting Help
- Check the documentation files
- Review browser console for errors
- Verify Supabase dashboard for issues
- Test with different browsers/devices

## 🎯 Roadmap

### Planned Features
- [ ] Expense categories
- [ ] Budget tracking
- [ ] Export functionality
- [ ] Multi-currency support
- [ ] Recurring expenses
- [ ] Analytics dashboard
- [ ] Push notifications

### Technical Improvements
- [ ] Unit tests
- [ ] E2E testing
- [ ] Performance monitoring
- [ ] Error tracking
- [ ] A/B testing framework

---

**Built with ❤️ for modern expense tracking**
