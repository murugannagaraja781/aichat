# Testing Guide

## Overview

Complete unit test suite for MERN WebRTC application covering:
- Backend API endpoints
- Socket.IO events
- MongoDB models
- React components
- WebRTC mocks

## Running Tests

### Backend Tests

```bash
# Install dependencies
npm install

# Run all backend tests
npm test

# Run tests in watch mode
npm run test:watch

# Run with coverage report
npm test -- --coverage
```

### Frontend Tests

```bash
# Navigate to client
cd client

# Install dependencies
npm install

# Run all frontend tests
npm test

# Run tests in watch mode
npm run test:watch

# Run with coverage
npm test -- --coverage
```

## Test Coverage

### Backend Tests (`tests/`)

**server.test.js**
- ✅ POST /api/room/create - Creates room with UUID
- ✅ POST /api/room/create - Returns unique IDs
- ✅ GET /api/room/:id/join - Returns existing room
- ✅ GET /api/room/:id/join - Returns 404 for invalid room
- ✅ Room model validation
- ✅ Room participants management

**socket.test.js**
- ✅ Socket connection
- ✅ join-room event
- ✅ offer event
- ✅ answer event
- ✅ ice-candidate event
- ✅ chat-message event
- ✅ raise-hand event
- ✅ toggle-audio event
- ✅ toggle-video event
- ✅ leave-room event

### Frontend Tests (`client/src/`)

**Home.test.jsx**
- ✅ Renders home page
- ✅ Input field updates
- ✅ Create room validation
- ✅ Join room validation
- ✅ API error handling
- ✅ Navigation after room creation
- ✅ Loading states

**Room.test.jsx**
- ✅ Renders room component
- ✅ Redirects without username
- ✅ Control buttons present
- ✅ Copy room link
- ✅ Toggle chat panel

**App.test.js**
- ✅ App renders without crashing
- ✅ Routes configured correctly

## Test Structure

```
project/
├── tests/                    # Backend tests
│   ├── server.test.js       # API endpoint tests
│   └── socket.test.js       # Socket.IO tests
├── client/
│   └── src/
│       ├── setupTests.js    # Test configuration
│       ├── App.test.js      # App component tests
│       └── pages/
│           ├── Home.test.jsx    # Home page tests
│           └── Room.test.jsx    # Room page tests
├── jest.config.js           # Backend Jest config
└── TEST_GUIDE.md           # This file
```

## Mocked APIs

### WebRTC APIs (Frontend)
- RTCPeerConnection
- RTCSessionDescription
- RTCIceCandidate
- navigator.mediaDevices.getUserMedia
- navigator.mediaDevices.getDisplayMedia

### Browser APIs (Frontend)
- localStorage
- navigator.clipboard
- window.alert

### Database (Backend)
- MongoDB Memory Server (in-memory database)

## Writing New Tests

### Backend Test Example

```javascript
describe('New Feature', () => {
  it('should do something', async () => {
    const response = await request(app)
      .post('/api/endpoint')
      .send({ data: 'test' })
      .expect(200);

    expect(response.body).toHaveProperty('result');
  });
});
```

### Frontend Test Example

```javascript
import { render, screen, fireEvent } from '@testing-library/react';

describe('Component', () => {
  it('should render and interact', () => {
    render(<Component />);
    const button = screen.getByText('Click Me');
    fireEvent.click(button);
    expect(screen.getByText('Clicked')).toBeInTheDocument();
  });
});
```

## CI/CD Integration

### GitHub Actions Example

```yaml
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '18'

      - name: Backend Tests
        run: |
          npm install
          npm test

      - name: Frontend Tests
        run: |
          cd client
          npm install
          npm test
```

## Coverage Reports

After running tests with coverage:

**Backend:**
```bash
npm test -- --coverage
# View: coverage/lcov-report/index.html
```

**Frontend:**
```bash
cd client
npm test -- --coverage
# View: coverage/lcov-report/index.html
```

## Troubleshooting

### Tests Timeout
- Increase timeout in jest.config.js
- Check for unresolved promises
- Ensure proper cleanup in afterAll/afterEach

### MongoDB Connection Issues
- mongodb-memory-server downloads MongoDB binary on first run
- May take time on slow connections
- Binary cached for subsequent runs

### WebRTC Mock Issues
- Ensure setupTests.js is loaded
- Check mock implementations match actual API
- Verify async operations are awaited

## Best Practices

1. **Isolation**: Each test should be independent
2. **Cleanup**: Always cleanup resources in afterEach/afterAll
3. **Mocking**: Mock external dependencies
4. **Coverage**: Aim for >80% coverage
5. **Descriptive**: Use clear test descriptions
6. **Fast**: Keep tests fast (<100ms each)
7. **Deterministic**: Tests should always produce same result

## Next Steps

- Add integration tests for full user flows
- Add E2E tests with Cypress/Playwright
- Add performance tests
- Add load testing for Socket.IO
- Add visual regression tests
