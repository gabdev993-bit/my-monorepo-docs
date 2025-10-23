# Authentication Setup Documentation

## Overview
This document outlines the complete authentication setup for the mobile app using Supabase as the backend and Google OAuth for authentication.

## Configuration Summary

### ✅ Supabase Backend
- **Project URL**: `https://mbneolqjelqrbxnetpcp.supabase.co`
- **Anonymous Key**: `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1ibmVvbHFqZWxxcmJ4bmV0cGNwIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjExNDMzNzksImV4cCI6MjA3NjcxOTM3OX0.X3h54JPFtjNCPLijFgNZdcZnIyj4Vdskb9QvdF1x75I`

### ✅ Google OAuth
- **Client ID**: `939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84.apps.googleusercontent.com`
- **iOS URL Scheme**: `com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84`
- **Reversed Client ID**: `com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84`

### ✅ App Deep Links
- **App Scheme**: `my-monorepo-mobile`
- **OAuth Redirect**: `my-monorepo-mobile://oauth`

## Environment Variables

### Required Environment Variables
```bash
# Supabase Configuration
EXPO_PUBLIC_SUPABASE_URL=https://mbneolqjelqrbxnetpcp.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im1ibmVvbHFqZWxxcmJ4bmV0cGNwIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjExNDMzNzksImV4cCI6MjA3NjcxOTM3OX0.X3h54JPFtjNCPLijFgNZdcZnIyj4Vdskb9QvdF1x75I

# Google OAuth Configuration
EXPO_PUBLIC_GOOGLE_IOS_URL_SCHEME=com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84
EXPO_PUBLIC_GOOGLE_REVERSED_CLIENT_ID=com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84
EXPO_PUBLIC_APP_DEEP_LINK_SCHEME=my-monorepo-mobile
```

## Configuration Files Updated

### 1. `app.json`
- Added Supabase credentials to `extra` section
- Added Google OAuth configuration
- Added app deep link scheme

### 2. `eas.json`
- Added environment variables for all build profiles (development, preview, production)
- Configured for consistent builds across environments

### 3. iOS Configuration (`ios/MyMonorepoMobile/Info.plist`)
- Added `CFBundleURLTypes` for deep link handling
- Configured app scheme: `my-monorepo-mobile`
- Configured Google OAuth scheme: `com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84`

### 4. Android Configuration (`android/app/src/main/AndroidManifest.xml`)
- Added intent filters for deep link handling
- Configured app scheme: `my-monorepo-mobile`
- Configured Google OAuth scheme: `com.googleusercontent.apps.939087202767-8j3bsdb26obnkfi85qtmml2m757hcc84`

## Authentication Service Implementation

### ✅ Completed Features
- **Google OAuth Flow**: Complete implementation with deep link handling
- **Supabase Integration**: Full session management with Supabase
- **User Management**: Get current user, auth state changes
- **Sign Out**: Complete sign out functionality
- **Authentication Check**: Session validation

### 🔧 Auth Service Functions
```typescript
// Sign in with Google OAuth
signInWithGoogle(): Promise<AuthResult>

// Sign out current user
signOut(): Promise<AuthResult>

// Get current authenticated user
getUser(): Promise<AuthUser | null>

// Listen to auth state changes
onAuthStateChange(callback: (user: AuthUser | null) => void): () => void

// Check if user is authenticated
isAuthenticated(): Promise<boolean>
```

## Next Steps

### 1. Google Cloud Console Configuration
- [ ] Add iOS bundle ID to Google OAuth credentials
- [ ] Add Android package name to Google OAuth credentials
- [ ] Configure authorized redirect URIs

### 2. Supabase Configuration
- [ ] Enable Google OAuth provider in Supabase Auth settings
- [ ] Add Google OAuth client ID to Supabase
- [ ] Configure OAuth redirect URLs

### 3. Testing
- [ ] Test OAuth flow on iOS simulator
- [ ] Test OAuth flow on Android emulator
- [ ] Test deep link handling
- [ ] Test session persistence

## Usage Example

```typescript
import { signInWithGoogle, signOut, getUser, onAuthStateChange } from './src/services/authService'

// Sign in with Google
const result = await signInWithGoogle()
if (result.success) {
  console.log('User signed in:', result.user)
}

// Listen to auth changes
const unsubscribe = onAuthStateChange((user) => {
  if (user) {
    console.log('User authenticated:', user)
  } else {
    console.log('User signed out')
  }
})

// Get current user
const user = await getUser()

// Sign out
await signOut()
```

## Security Notes

- ✅ Environment variables are properly configured
- ✅ Deep link schemes are secured
- ✅ OAuth tokens are handled securely through Supabase
- ✅ Session management is handled by Supabase
- ⚠️ Remember to configure production OAuth credentials in Google Cloud Console
- ⚠️ Ensure Supabase Auth settings are properly configured for production
