# WebRTC Video Calling System (MERN)

Full-featured P2P video calling application with WebRTC, Socket.IO, React, Node.js, Express, and MongoDB.

## Features

- ✅ Create/Join rooms with UUID
- ✅ P2P video + audio calling
- ✅ Multi-user support
- ✅ Mute/unmute audio
- ✅ Camera on/off
- ✅ Screen sharing
- ✅ Real-time chat
- ✅ Raise hand
- ✅ Join/leave notifications
- ✅ Auto-reconnect logic
- ✅ Responsive design

## Tech Stack

- **Frontend**: React, Socket.IO Client, WebRTC
- **Backend**: Node.js, Express, Socket.IO
- **Database**: MongoDB
- **Signaling**: Socket.IO

## Installation

### Prerequisites

- Node.js (v16+)
- MongoDB (local or Atlas)
- npm or yarn

### Backend Setup

```bash
# Install dependencies
npm install

# Create .env file
cp .env.example .env

# Edit .env with your MongoDB URI
# MONGODB_URI=mongodb://localhost:27017/webrtc-calls
# PORT=7009
# CLIENT_URL=http://localhost:3000

# Start MongoDB (if local)
mongod

# Run server
npm start

# Or development mode
npm run dev
```

### Frontend Setup

```bash
# Navigate to client
cd client

# Install dependencies
npm install

# Create .env file (optional)
# REACT_APP_API_URL=http://localhost:7009
# REACT_APP_SOCKET_URL=http://localhost:7009

# Start React app
npm start
```

## Usage

1. Open http://localhost:3000
2. Enter your name
3. Click "Create New Room" or enter a room ID to join
4. Share the room link with others
5. Use controls to manage audio/video/screen share

## Deployment

### Backend (Railway/Render/Heroku)

1. Push code to GitHub
2. Connect repository to Railway/Render
3. Set environment variables:
   - `MONGODB_URI`
   - `CLIENT_URL`
   - `PORT`
4. Deploy

### Frontend (Vercel/Netlify)

```bash
cd client
npm run build

# Deploy build folder
# Set environment variables:
# REACT_APP_API_URL=https://your-backend.railway.app
# REACT_APP_SOCKET_URL=https://your-backend.railway.app
```

## Production Considerations

1. **TURN Server**: Add TURN servers in `client/src/pages/Room.jsx` for NAT traversal
2. **HTTPS**: Required for getUserMedia() in production
3. **MongoDB Atlas**: Use cloud MongoDB for production
4. **Environment Variables**: Set all required env vars
5. **CORS**: Configure proper CORS origins
6. **Rate Limiting**: Add rate limiting to API endpoints
7. **Authentication**: Add user authentication if needed

## TURN Server Setup (Optional)

```javascript
// In Room.jsx, update iceServers:
const iceServers = {
  iceServers: [
    { urls: 'stun:stun.l.google.com:19302' },
    {
      urls: 'turn:your-turn-server.com:3478',
      username: 'username',
      credential: 'password'
    }
  ]
};
```

## API Endpoints

- `POST /api/room/create` - Create new room
- `GET /api/room/:id/join` - Check if room exists

## Socket Events

### Client → Server
- `join-room` - Join a room
- `offer` - Send WebRTC offer
- `answer` - Send WebRTC answer
- `ice-candidate` - Send ICE candidate
- `chat-message` - Send chat message
- `raise-hand` - Raise hand
- `toggle-audio` - Toggle audio state
- `toggle-video` - Toggle video state
- `leave-room` - Leave room

### Server → Client
- `all-users` - List of users in room
- `user-joined` - New user joined
- `user-left` - User left
- `offer` - Receive WebRTC offer
- `answer` - Receive WebRTC answer
- `ice-candidate` - Receive ICE candidate
- `chat-message` - Receive chat message
- `hand-raised` - User raised hand
- `user-audio-toggle` - User toggled audio
- `user-video-toggle` - User toggled video

## License

MIT
