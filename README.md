# Appliwaste - Waste Management Mobile Application

A React Native Expo application for waste identification and recycling center location.

## Project Structure

```
AWEXPO/
├── src/                    # Frontend React Native code
│   ├── screens/           # Application screens
│   ├── navigation/        # Navigation configuration
│   ├── constants/         # Design system (colors, typography)
│   ├── services/          # API services
│   └── types/             # TypeScript type definitions
├── backend/               # Node.js Express server
│   ├── models/           # MongoDB schemas
│   ├── routes/           # API endpoints
│   ├── middleware/       # Authentication & validation
│   └── server.js         # Main server file
├── assets/               # Images and static files
└── docker-compose.yml    # Docker configuration
```

## Frontend-Backend Connection

### API Service Layer
The frontend connects to the backend through `src/services/api.ts`:

- **Base URL**: `http://localhost:5000/api` (development)
- **Authentication**: JWT tokens stored in AsyncStorage
- **HTTP Client**: Axios with request/response interceptors
- **Error Handling**: Centralized error management

### Key API Endpoints
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User authentication
- `GET /api/auth/profile` - Get user profile
- `GET /api/health` - Server health check

### Authentication Flow
1. User registers/logs in through frontend
2. Backend validates credentials and returns JWT token
3. Frontend stores token in AsyncStorage
4. All subsequent API calls include token in Authorization header
5. Backend validates token and returns user data

## Engineer Override Feature

The Engineer Override is a development/testing feature that allows bypassing authentication:

### Purpose
- Skip login during development
- Test app functionality without backend
- Debug UI/UX without authentication issues

### Implementation
- Located in `src/screens/OnboardingScreen.tsx`
- Red "ENG OVERRIDE" link at bottom of login screen
- Calls `onComplete()` directly, bypassing authentication
- Only visible during development

### Usage
1. Navigate to login screen
2. Scroll to bottom
3. Tap "ENG OVERRIDE" link
4. App proceeds to main interface

## Installation & Setup

### Prerequisites
- Node.js (v16+)
- npm or yarn
- Expo CLI
- MongoDB Atlas account

### Frontend Setup
```bash
# Install dependencies
npm install

# Start Expo development server
npm start
```

### Backend Setup
```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Set environment variables
# Create .env file with MongoDB connection string

# Start server
npm run dev:cloud
```

### Environment Variables
Create `.env` file in backend directory:
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/database
JWT_SECRET=your_jwt_secret_key
PORT=5000
```

## Features

### Core Functionality
- User authentication (register/login)
- Camera integration for waste scanning
- Image upload and management
- Recycling center locator
- Waste categorization

### Design System
- Consistent color palette
- Typography hierarchy (Helvetica, Roboto, Courier)
- Responsive layouts
- Modern UI components

### Navigation
- Bottom tab navigation
- Stack navigation for screens
- Onboarding flow

## Development

### Adding New Features
1. Create screen in `src/screens/`
2. Add navigation route in `src/navigation/`
3. Create API endpoint in `backend/routes/`
4. Update API service in `src/services/`

### Styling Guidelines
- Use design system constants (`colors.ts`, `theme.ts`)
- Follow component structure patterns
- Maintain responsive design principles

## Deployment

### Docker Deployment
```bash
# Build and run with Docker
docker-compose up --build
```

### Production Considerations
- Update API base URL for production
- Configure environment variables
- Remove Engineer Override in production
- Set up proper MongoDB security

## Troubleshooting

### Common Issues
- Backend not running: Check if server is started on port 5000
- Authentication errors: Verify MongoDB connection
- Image upload issues: Check camera permissions
- Navigation problems: Verify route configurations

### Debug Mode
- Use Engineer Override to bypass auth issues
- Check browser console for API errors
- Verify environment variables are loaded
