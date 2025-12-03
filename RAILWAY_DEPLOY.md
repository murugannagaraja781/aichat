# Railway Deployment Guide (Separate Services)

This guide deploys backend and frontend as separate Railway services.

## Project Structure

```
/
├── backend/              ← Backend service (Railway)
│   ├── server.js
│   ├── models/
│   ├── package.json
│   └── railway.json
├── frontend/             ← Frontend service (Railway)
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── railway.json
└── package.json          ← Root (for local development)
```

## Prerequisites

### Setup MongoDB Atlas
1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free cluster
3. Create database user with password
4. Network Access → Add IP: `0.0.0.0/0`
5. Get connection string: `mongodb+srv://username:password@cluster.mongodb.net/webrtc-calls`

## Deployment Steps

### Step 1: Push to GitHub
```bash
git add .
git commit -m "Restructure for Railway deployment"
git push origin main
```

### Step 2: Deploy Backend

1. Go to [Railway](https://railway.app)
2. Click "New Project" → "Deploy from GitHub repo"
3. Select your repository
4. **Important:** Set Root Directory to `backend`
5. Railway will detect Node.js and deploy

**Environment Variables for Backend:**
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/webrtc-calls
NODE_ENV=production
CLIENT_URL=https://your-frontend.railway.app
```

6. Generate domain: Settings → Networking → Generate Domain
7. Copy backend URL (e.g., `https://backend-production-xxxx.railway.app`)

### Step 3: Deploy Frontend

1. In Railway dashboard, click "New" → "GitHub Repo"
2. Select the SAME repository
3. **Important:** Set Root Directory to `frontend`
4. Railway will detect Node.js and deploy

**Environment Variables for Frontend:**
```
REACT_APP_API_URL=https://backend-production-xxxx.railway.app
REACT_APP_SOCKET_URL=https://backend-production-xxxx.railway.app
```

5. Generate domain: Settings → Networking → Generate Domain
6. Copy frontend URL

### Step 4: Update Backend CLIENT_URL

1. Go back to backend service in Railway
2. Update `CLIENT_URL` variable with your frontend URL
3. Railway will auto-redeploy

## Final Configuration

**Backend Environment Variables:**
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/webrtc-calls
NODE_ENV=production
CLIENT_URL=https://frontend-production-xxxx.railway.app
```

**Frontend Environment Variables:**
```
REACT_APP_API_URL=https://backend-production-xxxx.railway.app
REACT_APP_SOCKET_URL=https://backend-production-xxxx.railway.app
```

## Verify Deployment

1. Visit your frontend Railway URL
2. Create a room
3. Open room link in another browser/tab
4. Test video call functionality

## Local Development

```bash
# Install all dependencies
npm run install:all

# Terminal 1 - Run backend
npm run dev:backend

# Terminal 2 - Run frontend
npm run dev:frontend
```

Backend runs on: http://localhost:7009
Frontend runs on: http://localhost:3000

## Troubleshooting

### Backend Issues
- Check Railway logs: Backend service → Deployments → View Logs
- Verify MONGODB_URI is correct
- Ensure MongoDB Atlas allows 0.0.0.0/0
- Check CORS settings allow frontend URL

### Frontend Issues
- Check Railway logs: Frontend service → Deployments → View Logs
- Verify REACT_APP_API_URL and REACT_APP_SOCKET_URL are correct
- Check browser console for errors
- Ensure environment variables are set before build

### Connection Issues
- Both services must use HTTPS (Railway provides this)
- Verify CLIENT_URL in backend matches frontend URL
- Check Socket.IO connection in browser dev tools
- Allow camera/microphone permissions

### Common Errors

**"Room not found"**
- Backend not connected to MongoDB
- Check MONGODB_URI

**"Cannot connect to server"**
- Frontend environment variables incorrect
- Check REACT_APP_API_URL

**"WebSocket connection failed"**
- Check REACT_APP_SOCKET_URL
- Verify CORS settings in backend

## Railway Services Overview

| Service | Port | URL | Purpose |
|---------|------|-----|---------|
| Backend | 7009 | backend-xxx.railway.app | API + Socket.IO |
| Frontend | Auto | frontend-xxx.railway.app | React App |

## Costs

- Railway Free Tier: $5 credit/month (500 hours)
- Each service uses separate hours
- MongoDB Atlas: Free tier (512MB)
- **Total: FREE** for small projects

## Scaling

Free tier per service:
- 512MB RAM
- 1GB disk
- Shared CPU

To scale:
- Upgrade to Railway Pro
- Add Redis for session management
- Add TURN server for better connectivity

## Custom Domains

**Backend:**
1. Railway → Backend service → Settings → Domains
2. Add custom domain (e.g., api.yourdomain.com)
3. Update DNS records
4. Update frontend REACT_APP_API_URL

**Frontend:**
1. Railway → Frontend service → Settings → Domains
2. Add custom domain (e.g., yourdomain.com)
3. Update DNS records
4. Update backend CLIENT_URL

## Monitoring

Railway Dashboard shows:
- CPU/Memory usage
- Request logs
- Build logs
- Deployment history
- Metrics

## Redeployment

Auto-deploy on git push (both services deploy automatically).

Manual redeploy:
1. Select service
2. Deployments → Click "Redeploy"

## Adding TURN Server (Optional)

Update `frontend/src/pages/Room.jsx`:

```javascript
const iceServers = {
  iceServers: [
    { urls: 'stun:stun.l.google.com:19302' },
    {
      urls: 'turn:turn.example.com:3478',
      username: 'username',
      credential: 'password'
    }
  ]
};
```

Free TURN services:
- Metered.ca
- Xirsys
- Twilio TURN
