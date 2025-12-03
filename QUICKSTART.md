# Quick Start Guide

## Prerequisites

```bash
node --version  # v16 or higher
npm --version   # v8 or higher
mongod --version  # v5 or higher
```

## Installation (5 minutes)

### Step 1: Clone and Install Backend

```bash
# Install backend dependencies
npm install

# Create environment file
cp .env.example .env

# Start MongoDB (if using local)
mongod

# Or use MongoDB Atlas (cloud)
# Update MONGODB_URI in .env with your Atlas connection string
```

### Step 2: Install Frontend

```bash
# Navigate to client
cd client

# Install dependencies
npm install

# Create environment file (optional)
cp .env.example .env
```

### Step 3: Run Application

**Terminal 1 - Backend:**
```bash
# From root directory
npm start
# Server runs on http://localhost:7009
```

**Terminal 2 - Frontend:**
```bash
# From root directory
cd client
npm start
# App opens at http://localhost:3000
```

## First Test

1. Open http://localhost:3000
2. Enter your name: "Alice"
3. Click "Create New Room"
4. Copy the room link
5. Open new incognito window
6. Paste room link
7. Enter name: "Bob"
8. Both users should see each other's video

## Troubleshooting

### Camera/Mic Not Working
- Check browser permissions
- Use HTTPS in production
- Try different browser

### Connection Failed
- Check MongoDB is running
- Verify .env configuration
- Check firewall settings

### No Video/Audio
- Check WebRTC compatibility
- Verify STUN server access
- Check network/NAT settings

### Socket Connection Error
- Verify backend is running on port 7009
- Check CORS configuration
- Verify CLIENT_URL in .env

## Next Steps

- Read README.md for full documentation
- Check DEPLOYMENT.md for production setup
- Add TURN servers for better connectivity
- Customize UI in client/src/pages/
- Add authentication if needed

## Common Commands

```bash
# Backend
npm start          # Start server
npm run dev        # Development mode with nodemon

# Frontend
cd client
npm start          # Development server
npm run build      # Production build
npm test           # Run tests

# Both
npm install        # Install dependencies
```

## File Structure

```
├── server.js              # Backend entry point
├── models/
│   └── Room.js           # MongoDB schema
├── client/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── Home.jsx  # Landing page
│   │   │   └── Room.jsx  # Video call room
│   │   └── App.js        # React router
│   └── public/
└── package.json
```
