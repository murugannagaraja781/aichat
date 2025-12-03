# Deployment Guide

## Railway Deployment (Backend)

1. Create account at railway.app
2. New Project → Deploy from GitHub
3. Select your repository
4. Add environment variables:
   ```
   MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/webrtc
   CLIENT_URL=https://your-frontend.vercel.app
   PORT=7009
   NODE_ENV=production
   ```
5. Deploy

## Vercel Deployment (Frontend)

1. Install Vercel CLI: `npm i -g vercel`
2. Navigate to client folder: `cd client`
3. Run: `vercel`
4. Set environment variables in Vercel dashboard:
   ```
   REACT_APP_API_URL=https://your-backend.railway.app
   REACT_APP_SOCKET_URL=https://your-backend.railway.app
   ```
5. Redeploy: `vercel --prod`

## MongoDB Atlas Setup

1. Create account at mongodb.com/cloud/atlas
2. Create cluster (free tier available)
3. Create database user
4. Whitelist IP: 0.0.0.0/0 (allow all)
5. Get connection string
6. Replace in MONGODB_URI

## Render Deployment (Alternative Backend)

1. Create account at render.com
2. New Web Service → Connect repository
3. Build Command: `npm install`
4. Start Command: `npm start`
5. Add environment variables (same as Railway)

## Netlify Deployment (Alternative Frontend)

1. Install Netlify CLI: `npm i -g netlify-cli`
2. Build: `cd client && npm run build`
3. Deploy: `netlify deploy --prod --dir=build`
4. Set environment variables in Netlify dashboard

## HTTPS Requirements

- Production requires HTTPS for getUserMedia()
- Railway/Vercel/Render/Netlify provide HTTPS automatically
- For custom domains, configure SSL certificates

## TURN Server (Production)

For better connectivity behind NATs/firewalls:

1. Use services like:
   - Twilio TURN
   - Xirsys
   - Metered.ca
   - Self-hosted coturn

2. Update `client/src/pages/Room.jsx`:
```javascript
const iceServers = {
  iceServers: [
    { urls: 'stun:stun.l.google.com:19302' },
    {
      urls: 'turn:turn.example.com:3478',
      username: 'your-username',
      credential: 'your-password'
    }
  ]
};
```

## Performance Optimization

1. Enable gzip compression
2. Add CDN for static assets
3. Implement connection pooling for MongoDB
4. Add Redis for session management (optional)
5. Monitor with services like New Relic or Datadog

## Security Checklist

- [ ] Enable CORS with specific origins
- [ ] Add rate limiting
- [ ] Implement authentication
- [ ] Validate all inputs
- [ ] Use environment variables for secrets
- [ ] Enable MongoDB authentication
- [ ] Add HTTPS redirect
- [ ] Implement room passwords (optional)
- [ ] Add user session management
