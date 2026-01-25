# Vercel Deployment

Deploy RushChat frontend application using Vercel.

## Vercel Deployment Overview

```markmap
# Vercel Deployment
## Prerequisites
- Vercel Account
- GitHub Account
- Code Pushed
## Deployment Steps
- Create Project
  - Add New Project
  - Select Repository
  - Configure Root Directory: client
- Configure Project
  - Framework: Create React App
  - Build Command: npm run build
  - Output Directory: build
- Configure Environment Variables
  - REACT_APP_API_URL
  - REACT_APP_SOCKET_URL
- Deploy
  - Click Deploy
  - Auto Build
  - Get URL
## Custom Domain
- Add Domain
- Configure DNS
- SSL Certificate
## Auto Deployment
- GitHub Integration
- Auto Trigger
- Preview Deployment
```

## Prerequisites

- Vercel account (https://vercel.com/)
- GitHub account
- Code pushed to GitHub

## Deployment Steps

### 1. Create Vercel Project

1. Log in to Vercel
2. Click "Add New Project"
3. Select RushChat repository
4. Configure project settings:
   - **Framework Preset**: Create React App
   - **Root Directory**: `client`
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`

### 2. Configure Environment Variables

Add environment variables in project settings:

```env
REACT_APP_API_URL=https://your-backend.railway.app
REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

### 3. Deploy

1. Click "Deploy"
2. Vercel will automatically build and deploy
3. Wait for deployment to complete
4. Get deployment URL

### 4. Configure Custom Domain

1. In project settings
2. Click "Domains"
3. Add custom domain
4. Configure DNS records

## Auto Deployment

### GitHub Integration

Vercel automatically:

- Monitors GitHub pushes
- Automatically triggers deployment
- Generates preview deployments (Pull Request)

### Preview Deployment

Each Pull Request generates a preview deployment:

- Independent deployment URL
- For testing and preview
- Does not affect production environment

## Build Optimization

### Environment Variables

Ensure all environment variables are configured:

- `REACT_APP_API_URL`
- `REACT_APP_SOCKET_URL`
- Other frontend required variables

### Build Configuration

Vercel automatically optimizes:

- Code splitting
- Resource compression
- CDN distribution

## Troubleshooting

### Build Failed

- Check Node.js version
- Check if dependencies are correct
- View build logs

### Runtime Errors

- Check environment variables
- Check API URL configuration
- View browser console

### CORS Error

- Check backend CORS configuration
- Ensure `CLIENT_URL` is correct
- Check if domain matches

## Related Documentation

- [Deployment Overview](overview.md)
- [Environment Variables](environment.md)
