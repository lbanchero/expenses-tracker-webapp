# Supabase Setup Guide for Expense Tracker PWA

## Step 1: Create Supabase Project

1. Go to [supabase.com](https://supabase.com) and sign up/sign in
2. Click "New Project"
3. Choose your organization
4. Fill in project details:
   - Name: "Expense Tracker"
   - Database Password: (generate a strong password and save it)
   - Region: Choose closest to your users
5. Click "Create new project"
6. Wait for project to be ready (2-3 minutes)

## Step 2: Get Project Credentials

1. In your Supabase dashboard, go to Settings > API
2. Copy these values (you'll need them later):
   - Project URL (e.g., https://your-project.supabase.co)
   - Anon public key (starts with "eyJ...")

## Step 3: Set Up Google OAuth

### 3.1 Google Cloud Console Setup
1. Go to [Google Cloud Console](https://console.cloud.google.com)
2. Create a new project or select existing one
3. Enable Google+ API:
   - Go to "APIs & Services" > "Library"
   - Search for "Google+ API" and enable it
4. Create OAuth 2.0 credentials:
   - Go to "APIs & Services" > "Credentials"
   - Click "Create Credentials" > "OAuth 2.0 Client IDs"
   - Configure OAuth consent screen if prompted
   - Application type: "Web application"
   - Name: "Expense Tracker"
   - Authorized redirect URIs: `https://your-project.supabase.co/auth/v1/callback`
5. Copy Client ID and Client Secret

### 3.2 Supabase OAuth Configuration
1. In Supabase dashboard, go to Authentication > Providers
2. Find Google provider and click to configure
3. Enable Google provider
4. Enter your Google Client ID and Client Secret
5. Click "Save"

## Step 4: Database Schema Setup

Run this SQL in your Supabase SQL Editor (Database > SQL Editor):

```sql
-- Create transactions table
CREATE TABLE transactions (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    user_id UUID REFERENCES auth.users(id) ON DELETE CASCADE,
    amount DECIMAL(10,2) NOT NULL CHECK (amount > 0),
    description TEXT NOT NULL,
    transaction_date DATE NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE transactions ENABLE ROW LEVEL SECURITY;

-- Create policy for users to only access their own transactions
CREATE POLICY "Users can only access their own transactions" ON transactions
    FOR ALL USING (auth.uid() = user_id);

-- Create index for better performance
CREATE INDEX idx_transactions_user_date ON transactions(user_id, transaction_date DESC);
```

## Step 5: Configure Site URL (for deployment)

1. In Supabase dashboard, go to Authentication > URL Configuration
2. Add your site URL:
   - For development: `http://localhost:3000`
   - For production: `https://your-app.ondigitalocean.app`
3. Add redirect URLs:
   - `http://localhost:3000/**`
   - `https://your-app.ondigitalocean.app/**`

## Environment Variables

You'll need these values for your app:
- `SUPABASE_URL`: Your project URL
- `SUPABASE_ANON_KEY`: Your anon public key

Save these securely - you'll add them to your application next!
