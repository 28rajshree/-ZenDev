# ZenDev
# ZenDev - AI-Powered Meditation App for Developers

**Peaceful code, peaceful mind.** A meditation sanctuary designed specifically for software developers and tech professionals.

![ZenDev Landing Page](https://images.unsplash.com/photo-1760454220892-2fe92960cb29?crop=entropy&cs=srgb&fm=jpg&w=1200)

## 🌲 Overview

ZenDev is a full-stack meditation application that combines AI-powered personalized meditation scripts with progress tracking and mindfulness tools. Built with React, FastAPI, and MongoDB, it features a calming, earthy design aesthetic that promotes focus and tranquility.

## ✨ Features

### Core Functionality
- **AI-Generated Meditation Scripts**: Personalized meditation guidance powered by OpenAI GPT-5.2, tailored to your mood and goals
- **Progress Tracking**: Monitor your meditation journey with detailed session history
- **Streak System**: Build consistency with daily meditation streaks
- **Timer & Controls**: Guided meditation sessions with play/pause functionality
- **Daily Reminders**: Set customizable meditation reminders to maintain your practice

### User Experience
- **Authentication**: Secure JWT-based user authentication with bcrypt password hashing
- **Theme Toggle**: Switch between light and dark modes with persistent preferences
- **Responsive Design**: Beautiful UI that works seamlessly on mobile and desktop
- **Dashboard**: Comprehensive stats showing total sessions, minutes meditated, and streaks

## 🎨 Design

ZenDev features an organic, earthy design language:
- **Color Palette**: Deep forest green, warm sand tones, and natural accents
- **Typography**: Fraunces serif for headings, Inter for body text, JetBrains Mono for stats
- **Visual Style**: Calm, minimal, and grounded with subtle textures and animations
- **Theme**: Dark mode by default with light mode support

## 🛠️ Tech Stack

### Frontend
- **React** 19.0.0 with React Router for navigation
- **Tailwind CSS** with custom design tokens
- **Shadcn UI** components for consistent, accessible interface
- **Axios** for API communication
- **Sonner** for toast notifications

### Backend
- **FastAPI** with async/await support
- **MongoDB** with Motor (async driver)
- **JWT** authentication with bcrypt
- **OpenAI GPT-5.2** via emergentintegrations library
- **Pydantic** for data validation

### Infrastructure
- **Docker** containerized environment
- **Supervisor** for process management
- **Kubernetes** ingress routing

## 📁 Project Structure

```
/app
├── backend/
│   ├── server.py              # FastAPI application with all routes
│   ├── requirements.txt       # Python dependencies
│   └── .env                   # Environment variables
├── frontend/
│   ├── src/
│   │   ├── pages/
│   │   │   ├── LandingPage.js      # Hero page with features
│   │   │   ├── AuthPage.js         # Login/Register
│   │   │   ├── Dashboard.js        # Stats & overview
│   │   │   ├── MeditationSession.js # AI script generation & timer
│   │   │   ├── Settings.js         # Preferences & theme
│   │   │   └── History.js          # Session history
│   │   ├── components/ui/     # Shadcn UI components
│   │   ├── App.js             # Main app with routing
│   │   ├── App.css            # Custom animations
│   │   └── index.css          # Tailwind & theme
│   ├── package.json
│   ├── tailwind.config.js
│   └── .env
└── README.md
```

## 🚀 Getting Started

### Prerequisites
- Python 3.11+
- Node.js 18+
- MongoDB
- OpenAI API key (or use Emergent LLM Key)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/zendev.git
cd zendev
```

2. **Backend Setup**
```bash
cd backend
pip install -r requirements.txt

# Configure environment variables in .env
MONGO_URL=\"mongodb://localhost:27017\"
DB_NAME=\"zendev_db\"
EMERGENT_LLM_KEY=your_key_here
JWT_SECRET=your_secret_key
CORS_ORIGINS=\"*\"
```

3. **Frontend Setup**
```bash
cd frontend
yarn install

# Configure environment variables in .env
REACT_APP_BACKEND_URL=http://localhost:8001
```

4. **Run the Application**
```bash
# Terminal 1 - Backend
cd backend
uvicorn server:app --host 0.0.0.0 --port 8001 --reload

# Terminal 2 - Frontend
cd frontend
yarn start
```

5. **Access the App**
- Frontend: http://localhost:3000
- Backend API: http://localhost:8001/api

## 🔐 API Endpoints

### Authentication
- `POST /api/auth/register` - Create new user account
- `POST /api/auth/login` - Login with credentials
- `GET /api/user/profile` - Get user profile (protected)

### Meditation
- `POST /api/meditation/generate-script` - Generate AI meditation script (protected)
- `POST /api/meditation/complete-session` - Save completed session (protected)
- `GET /api/meditation/history` - Get session history (protected)

### Dashboard & Stats
- `GET /api/dashboard/stats` - Get user stats and streaks (protected)

### Preferences
- `GET /api/preferences` - Get user preferences (protected)
- `PUT /api/preferences/reminder` - Update reminder settings (protected)
- `PUT /api/preferences/duration` - Update preferred duration (protected)

## 📊 Database Schema

### Collections

**users**
```javascript
{
  id: String,
  name: String,
  email: String,
  password: String (hashed),
  created_at: ISOString
}
```

**meditation_sessions**
```javascript
{
  id: String,
  user_id: String,
  duration: Number,
  script: String,
  mood: String,
  completed_at: ISOString
}
```

**streaks**
```javascript
{
  user_id: String,
  current_streak: Number,
  longest_streak: Number,
  last_session_date: ISOString
}
```

**preferences**
```javascript
{
  user_id: String,
  reminder: {
    enabled: Boolean,
    time: String,
    frequency: String
  },
  preferred_duration: Number,
  meditation_goals: Array<String>
}
```

## 🎯 Key Features Explained

### AI Meditation Script Generation
The app uses OpenAI's GPT-5.2 model to generate personalized meditation scripts based on:
- User's current mood (calm, stressed, tired, energetic, sad, grateful)
- Session duration (3-20 minutes)
- Meditation goals (mindfulness, relaxation, focus)

### Streak Tracking Algorithm
- Sessions on consecutive days increment the streak
- Sessions on the same day don't affect the streak
- Missing a day resets the streak to 1 (when next session completed)
- Longest streak is always preserved

### Theme System
- Uses CSS custom properties for theme colors
- Dark mode by default (developer-friendly)
- Preferences stored in localStorage
- Smooth transitions between themes

## 🧪 Testing

The application includes comprehensive testing:
- Backend API tests for all endpoints
- Frontend flow testing with Playwright
- Authentication and authorization tests
- AI integration validation

Run tests:
```bash
# Backend tests
python backend_test.py

# Frontend E2E tests (if configured)
yarn test
```

## 🔒 Security

- Passwords hashed with bcrypt
- JWT tokens with 30-day expiration
- HTTP-only authentication
- CORS configuration for production
- Environment variables for sensitive data
- MongoDB _id exclusion to prevent serialization errors

## 🌟 Future Enhancements

- Push notifications for daily reminders
- Ambient background sounds during meditation
- Social features (share streaks, group meditations)
- Meditation categories and guided programs
- Apple Health / Google Fit integration
- Voice-guided meditation playback
- Meditation insights and analytics
- Customizable meditation backgrounds

## 📝 License

This project is created as a portfolio/learning project.

## 👨‍💻 Author

Built with care for developers seeking peace and mindfulness.

**Ready to begin your journey?** Start meditating with ZenDev today and bring tranquility to your development workflow.
"
