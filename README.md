# WebRTC Video Calling System

A full-stack MERN application for real-time video calling using WebRTC, Socket.IO, and MongoDB.

## Project Structure

```
/
├── backend/              # Express + Socket.IO server
│   ├── server.js        # Main server file
│   ├── models/          # MongoDB models
│   ├── tests/           # Backend tests
│   └── package.json     # Backend dependencies
│
├── frontend/            # React application
│   ├── src/            # React components
│   ├── public/         # Static files
│   └── package.json    # Frontend dependencies
│
└── package.json        # Root scripts for development
```

## Features

- ✅ Real-time video calling with WebRTC
- ✅ Socket.IO for signaling
- ✅ MongoDB for room persistence
- ✅ Text chat during calls
- ✅ Raise hand feature
- ✅ Toggle audio/video
- ✅ Responsive design

## Local Development

### Prerequisites
- Node.js 16+
- MongoDB (local or Atlas)
- npm or yarn

### Setup

1. **Clone repository**
```bash
git clone <your-repo-url>
cd webrtc-video-call
```

2. **Install dependencies**
```bash
npm run install:all
```

3. **Configure Backend**
```bash
cd backend
cp .env.example .env
```

Edit `backend/.env`:
```env
PORT=7009
MONGODB_URI=mongodb://localhost:27017/webrtc-calls
CLIENT_URL=http://localhost:3000
NODE_ENV=development
```

4. **Configure Frontend**
```bash
cd frontend
cp .env.example .env
```

Edit `frontend/.env`:
```env
REACT_APP_API_URL=http://localhost:7009
REACT_APP_SOCKET_URL=http://localhost:7009
```

5. **Run Development Servers**

Terminal 1 - Backend:
```bash
npm run dev:backend
```

Terminal 2 - Frontend:
```bash
npm run dev:frontend
```

6. **Access Application**
- Frontend: http://localhost:3000
- Backend API: http://localhost:7009

## Testing

```bash
# Test backend
npm run test:backend

# Test frontend
npm run test:frontend
```

## Deployment

See [RAILWAY_DEPLOY.md](./RAILWAY_DEPLOY.md) for detailed Railway deployment instructions.

### Quick Deploy Summary

1. **Backend Service**
   - Root Directory: `backend`
   - Environment: MONGODB_URI, NODE_ENV, CLIENT_URL

2. **Frontend Service**
   - Root Directory: `frontend`
   - Environment: REACT_APP_API_URL, REACT_APP_SOCKET_URL

## API Endpoints

### REST API
- `POST /api/room/create` - Create new room
- `GET /api/room/:id/join` - Join existing room

### Socket.IO Events
- `join-room` - Join video room
- `offer` - WebRTC offer
- `answer` - WebRTC answer
- `ice-candidate` - ICE candidate exchange
- `chat-message` - Send chat message
- `raise-hand` - Raise hand notification
- `toggle-audio` - Toggle audio state
- `toggle-video` - Toggle video state
- `leave-room` - Leave room
- `disconnect` - User disconnected

## Tech Stack

**Backend:**
- Node.js + Express
- Socket.IO
- MongoDB + Mongoose
- CORS

**Frontend:**
- React 18
- React Router
- Socket.IO Client
- WebRTC API

## Browser Support

- Chrome 80+
- Firefox 75+
- Safari 14+
- Edge 80+

**Note:** HTTPS required for getUserMedia() in production.

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## License

ISC

## Support

For issues and questions, please open a GitHub issue.
