# Railway Deployment Guide

## Quick Deploy Steps

### 1. Prepare MongoDB Atlas
1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free cluster
3. Create a database user with password
4. Network Access → Add IP: `0.0.0.0/0` (allow from anywhere)
5. Copy your connection string (looks like: `mongodb+srv://username:password@cluster.mongodb.net/`)

### 2. Deploy Backend to Railway
1. Go to [Railway](https://railway.app)
2. Sign up/Login with GitHub
3. Click "New Project" → "Deploy from GitHub repo"
4. Select your repository
5. Railway will auto-detect Node.js and deploy

### 3. Configure Environment Variables
In Railway dashboard, go to Variables tab and add:

```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/webrtc-calls
CLIENT_URL=https://your-frontend-url.vercel.app
PORT=7009
NODE_ENV=production
```

**Note:** You'll update `CLIENT_URL` after deploying the frontend.

### 4. Get Your Backend URL
- Railway will provide a URL like: `https://your-app.railway.app`
- Copy this URL for the next step

### 5. Deploy Frontend to Vercel
1. Go to [Vercel](https://vercel.com)
2. Import your GitHub repository
3. Set Root Directory to: `client`
4. Add Environment Variables:
   ```
   REACT_APP_API_URL=https://your-app.railway.app
   REACT_APP_SOCKET_URL=https://your-app.railway.app
   ```
5. Deploy

### 6. Update Backend CLIENT_URL
1. Go back to Railway dashboard
2. Update `CLIENT_URL` variable with your Vercel URL
3. Railway will automatically redeploy

## Verify Deployment

1. Visit your Vercel frontend URL
2. Create a room
3. Open the room link in another browser/tab
4. Test video call functionality

## Troubleshooting

### Backend Issues
- Check Railway logs: Dashboard → Deployments → View Logs
- Verify MongoDB connection string is correct
- Ensure PORT is set to 7009

### Frontend Issues
- Check Vercel logs in deployment dashboard
- Verify environment variables are set correctly
- Check browser console for errors

### WebRTC Connection Issues
- Ensure both URLs use HTTPS
- Check browser permissions for camera/microphone
- For production, consider adding a TURN server (see DEPLOYMENT.md)

## Cost
- Railway: Free tier includes 500 hours/month
- Vercel: Free tier for personal projects
- MongoDB Atlas: Free tier (512MB storage)

## Custom Domain (Optional)
1. Railway: Settings → Domains → Add custom domain
2. Vercel: Settings → Domains → Add domain
3. Update environment variables accordingly
