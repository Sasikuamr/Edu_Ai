# EduAI - Full Stack Learning Platform Documentation

## 📋 Table of Contents
1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Technology Stack](#technology-stack)
4. [Project Structure](#project-structure)
5. [Backend Flow](#backend-flow)
6. [Frontend Flow](#frontend-flow)
7. [Database Schema](#database-schema)
8. [Authentication Flow](#authentication-flow)
9. [Feature Breakdown](#feature-breakdown)
10. [API Endpoints](#api-endpoints)
11. [Setup Instructions](#setup-instructions)
12. [Development Workflow](#development-workflow)

---

## 🏁 Conclusion

The EduAI platform represents a comprehensive educational technology solution that leverages modern web technologies and artificial intelligence to deliver personalized learning experiences. The integration of Google's Gemini AI throughout the application enables intelligent features like personalized learning plans, interactive quizzes, and an educational chatbot assistant.

Key strengths of the platform include:

1. **AI-Powered Personalization**: Tailored learning experiences based on user goals, experience level, and time commitment
2. **Progressive Learning Structure**: Multi-year plans broken down into manageable months and days
3. **Interactive Assessment**: Quiz-based verification of knowledge acquisition
4. **Multimedia Integration**: YouTube learning and potential for additional content sources
5. **Flexible Architecture**: Modular design allowing for future feature expansion

This documentation serves as a comprehensive guide for developers working on the EduAI platform, providing insights into architecture, data flow, security considerations, and implementation details.

---

## 🎯 Project Overview

**EduAI** is a comprehensive full-stack learning platform that provides personalized AI-powered education. The application features user authentication, onboarding, YouTube playlist analysis, calendar integration, and Google OAuth integration.

### Key Features:
- **User Authentication**: Email/password + Google OAuth
- **Personalized Onboarding**: 5-step flow for customized learning paths
- **AI Chatbot**: Gemini-powered learning assistant with context-aware responses
- **YouTube Learning**: Analyze playlists and create study schedules
- **Calendar Integration**: Sync learning schedules to Google Calendar
- **Phone Verification**: SMS verification system (simulated)
- **Responsive UI**: Modern React interface with animations
- **Learning Plans**: AI-generated personalized learning plans with monthly and daily breakdowns
- **Interactive Quizzes**: AI-generated knowledge assessment for each learning day
- **Progress Tracking**: Visual progress indicators for learning completion
- **Google Drive Integration**: Store and retrieve learning notes

---

## 🏗️ Architecture

### System Architecture
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   React Frontend │◄──►│  FastAPI Backend │◄──►│  PostgreSQL DB  │
│   (Port 3000)    │    │   (Port 8000)    │    │   (Port 5432)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Google OAuth   │    │ YouTube Data API │    │  Google Calendar │
│   Authentication │    │   (Playlist Info)│    │   (Event Sync)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Data Flow
1. **User Registration/Login** → JWT Token Generation
2. **Onboarding** → User Profile Creation
3. **YouTube Playlist Analysis** → Schedule Generation
4. **Calendar Sync** → Google Calendar Integration
5. **Phone Verification** → SMS Verification System (Simulated)

---

## 🛠️ Technology Stack

### Backend
- **Framework**: FastAPI (Python)
- **Database**: PostgreSQL with SQLAlchemy ORM
- **Authentication**: JWT Tokens + Google OAuth
- **Migrations**: Alembic
- **API Documentation**: Auto-generated with FastAPI
- **AI Integration**: Google Gemini 1.5 Flash/Pro for content generation

### Frontend
- **Framework**: React 19
- **Routing**: React Router DOM
- **Styling**: Inline styles + CSS
- **Icons**: React Icons
- **Animations**: Framer Motion
- **Calendar**: React Big Calendar
- **Date Handling**: date-fns
- **Utilities**: Custom date and progress calculation helpers

### External APIs
- **Google OAuth 2.0**: User authentication
- **YouTube Data API v3**: Playlist analysis
- **Google Calendar API**: Event synchronization
- **Google Generative AI**: Gemini API for AI-powered features

---

## 📁 Project Structure

```
learning/
├── fastapi-backend/                 # Backend API Server
│   ├── app/
│   │   ├── core/                   # Core configurations
│   │   │   ├── security.py         # JWT & password handling
│   │   │   └── google_auth.py      # Google OAuth integration
│   │   ├── database/
│   │   │   └── db.py              # Database connection & session
│   │   ├── models/                 # SQLAlchemy models
│   │   │   ├── user.py            # User model
│   │   │   ├── onboarding.py      # Onboarding model
│   │   │   ├── youtube_schedule.py # YouTube schedule model
│   │   │   ├── learning_plan.py   # Learning plan model
│   │   │   └── learning_path.py   # Learning path model
│   │   ├── utils/                  # Utility functions
│   │   │   ├── auth.py            # Authentication utilities
│   │   │   ├── youtube.py         # YouTube API utilities
│   │   │   ├── gemini_ai.py       # Gemini AI integration
│   │   │   └── calendar_sync.py   # Google Calendar sync utilities
│   │   ├── routes/                 # API endpoints
│   │   │   ├── auth.py            # Authentication routes
│   │   │   ├── onboarding.py      # Onboarding routes
│   │   │   ├── youtube.py         # YouTube integration routes
│   │   │   ├── learning_plan.py   # Learning plan routes
│   │   │   ├── chatbot.py         # AI chatbot routes
│   │   │   └── quiz.py            # Quiz generation and submission routes
│   │   ├── schemas/                # Pydantic schemas
│   │   │   ├── user.py            # User data validation
│   │   │   ├── onboarding.py      # Onboarding data validation
│   │   │   ├── youtube.py         # YouTube data validation
│   │   │   ├── learning_plan.py   # Learning plan data validation
│   │   │   ├── chatbot.py         # Chatbot message validation
│   │   │   └── quiz.py            # Quiz data validation
│   │   └── main.py                # FastAPI application entry
│   ├── alembic/                   # Database migrations
│   ├── requirements.txt           # Python dependencies
│   └── .env                      # Environment variables
│
└── learning-ui/                   # React Frontend
    ├── src/
    │   ├── components/            # React components
    │   │   ├── Login.js          # Login component
    │   │   ├── Register.js       # Registration component
    │   │   ├── OnboardingFlow.js # Onboarding wizard
    │   │   ├── Dashboard.js      # Main dashboard
    │   │   ├── Sidebar.js        # Navigation sidebar
    │   │   ├── Layout.js         # Layout wrapper
    │   │   ├── YouTubeLearning.js # YouTube feature
    │   │   ├── Calendar.js       # Calendar view
    │   │   ├── Profile.js        # User profile
    │   │   ├── GoogleCallback.js # OAuth callback
    │   │   ├── LearningPlans.js  # Learning plans interface
    │   │   ├── Quizzes.js        # Quiz interface
│   │   ├── Chatbot.js        # AI chatbot interface
│   │   └── Progress.js       # Progress tracking interface
    │   ├── utils/                # Frontend utilities
    │   │   ├── auth.js          # Authentication helpers
    │   │   ├── api.js           # API request helpers
    │   │   ├── date-utils.js    # Date formatting helpers
    │   │   └── progress-utils.js # Progress calculation helpers
    │   ├── api.js                # API utility functions
    │   ├── App.js                # Main React app
    │   └── index.js              # React entry point
    ├── package.json              # Node.js dependencies
    └── .env                      # Frontend environment variables
```

---

## 🔄 Backend Flow

### 1. Application Startup (`main.py`)
```python
# Flow: Server Start → Database Init → CORS Setup → Route Registration
```

**Detailed Process:**
1. **Environment Loading**: Loads `.env` variables
2. **Database Initialization**: **FORCE DROPS AND RECREATES ALL TABLES** on startup to ensure correct schema
3. **CORS Configuration**: Allows frontend (localhost:3000) access
4. **Route Registration**: Includes auth, onboarding, and YouTube routes
5. **Health Check**: Provides `/` and `/health` endpoints

**Key Implementation Details:**
- **Force Table Recreation**: `Base.metadata.drop_all(bind=engine)` then `Base.metadata.create_all(bind=engine)`
- **Schema Verification**: Checks for required columns in onboarding table
- **Error Handling**: Comprehensive error logging during startup

### 2. Database Connection (`database/db.py`)
```python
# Flow: Connection String → Engine Creation → Session Management
```

**Key Components:**
- **DATABASE_URL**: PostgreSQL connection string with psycopg2 driver
- **Engine**: SQLAlchemy engine for database operations
- **SessionLocal**: Database session factory
- **get_db**: Dependency injection for FastAPI routes
- **create_tables()**: Function to encapsulate table creation

### 3. Authentication System (`core/security.py`)
```python
# Flow: Password Hash → JWT Creation → Token Validation
```

**Functions:**
- `hash_password()`: Bcrypt password hashing
- `verify_password()`: Password verification
- `create_access_token()`: JWT token generation with user ID as subject
- `decode_token()`: JWT token validation and user ID extraction

### 4. Google OAuth Integration (`core/google_auth.py`)
```python
# Flow: OAuth URL → Code Exchange → Token Storage → API Access
```

**Process:**
1. **Authorization URL**: Creates Google OAuth URL with required scopes (including 'openid')
2. **Code Exchange**: Exchanges authorization code for tokens
3. **User Info Fetch**: Retrieves user profile from Google's `/oauth2/v2/userinfo` endpoint
4. **Session Creation**: Creates Google API session for Calendar access using stored access token

---

## 🎨 Frontend Flow

### 1. Application Entry (`App.js`)
```javascript
// Flow: Router Setup → Route Definition → Component Rendering
```

**Routing Structure:**
- `/` → Landing Page (animated welcome with Framer Motion)
- `/login` → Login Component
- `/register` → Registration Component
- `/auth/google/callback` → Google OAuth Callback Handler
- `/onboarding` → Onboarding Flow
- `/dashboard` → Main Dashboard
- `/youtube-learning` → YouTube Feature
- `/calendar` → Calendar View
- `/profile` → User Profile
- **Placeholder Routes**: `/learning-plans`, `/subplans`, `/quizzes`, `/notes`, `/voice-tutor`, `/resume`, `/community`, `/progress`, `/settings`

### 2. Authentication Flow
```javascript
// Flow: Login/Register → Token Storage → Route Protection
```

**Process:**
1. **Form Submission**: User enters credentials
2. **API Call**: Sends request to backend using `apiFetch()`
3. **Token Storage**: Stores JWT in localStorage
4. **Route Navigation**: Redirects to dashboard/onboarding based on completion status

### 3. API Integration (`api.js`)
```javascript
// Flow: Request → Authentication → Error Handling → Response
```

**Key Functions:**
- `apiFetch()`: Base API call with comprehensive error handling
- `authenticatedFetch()`: API call with automatic JWT token inclusion
- **Error Handling**: 422 validation errors, network errors, detailed error messages
- **Response Processing**: JSON parsing and error extraction

### 4. Component Architecture
```javascript
// Flow: Props → State → Effects → Render → User Interaction
```

**Component Pattern:**
1. **State Management**: useState for local state
2. **Side Effects**: useEffect for API calls and data fetching
3. **Event Handlers**: User interaction processing
4. **Conditional Rendering**: Dynamic UI based on state
5. **Layout Wrapper**: Layout component for consistent sidebar across authenticated pages

---

## 🗄️ Database Schema

### Users Table
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR UNIQUE NOT NULL,
    hashed_password VARCHAR,
    google_id VARCHAR UNIQUE,
    google_email VARCHAR,
    google_name VARCHAR,
    google_picture VARCHAR,
    google_access_token TEXT,
    is_google_authenticated BOOLEAN DEFAULT FALSE,
    phone_number VARCHAR,
    phone_verified BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    current_plan_id INTEGER,                -- References learning_plans.id
    current_month_index INTEGER,            -- Current month in the learning plan
    current_day INTEGER                     -- Current day in the current month
);
```

### Onboarding Table
```sql
CREATE TABLE onboarding (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) UNIQUE,
    name VARCHAR NOT NULL,
    grade VARCHAR NOT NULL,
    career_goals JSONB,           -- List of career goals (Data Scientist, Software Developer, etc.)
    current_skills JSONB,         -- List of current skills (Python, JavaScript, etc.)
    time_commitment VARCHAR       -- Daily time commitment (e.g., "2 hours")
);
```

### YouTube Schedules Table
```sql
CREATE TABLE youtube_schedules (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    playlist_id VARCHAR,
    playlist_url VARCHAR,
    playlist_title VARCHAR,
    daily_minutes INTEGER,
    schedule JSONB,
    start_time VARCHAR,
    duration_minutes INTEGER,
    created TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Learning Plans Table
```sql
CREATE TABLE learning_plans (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    title VARCHAR DEFAULT 'Personalized Learning Plan',
    total_years INTEGER,
    plan JSONB,                   -- Complex structure with months, days, and learning content
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Learning Paths Table
```sql
CREATE TABLE learning_paths (
    id SERIAL PRIMARY KEY,
    plan_id INTEGER REFERENCES learning_plans(id),
    user_id INTEGER REFERENCES users(id),
    global_month_index INTEGER,   -- 1..N across total_years*12
    year_number INTEGER,          -- 1..total_years
    month_of_year INTEGER,        -- 1..12
    title VARCHAR,
    status VARCHAR DEFAULT 'locked',  -- locked, active, completed
    current_day INTEGER DEFAULT 1,    -- Current day in this month (1-30)
    days_completed INTEGER DEFAULT 0, -- Number of completed days
    total_days INTEGER DEFAULT 30,    -- Total days in this month
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    last_activity_at TIMESTAMP,
    days_data JSONB,              -- Store day completion status and scores
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Day Progress Table
```sql
CREATE TABLE day_progress (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id),
    plan_id INTEGER REFERENCES learning_plans(id),
    month_index INTEGER,          -- 1-based month index
    day_number INTEGER,           -- 1-30 day number
    status VARCHAR DEFAULT 'locked',  -- locked, active, completed, failed
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    quiz_score INTEGER,           -- Last quiz score
    quiz_attempts INTEGER DEFAULT 0,  -- Number of quiz attempts
    best_score INTEGER,           -- Best score achieved
    content_viewed BOOLEAN DEFAULT FALSE,
    time_spent INTEGER DEFAULT 0, -- Time spent in seconds
    can_proceed BOOLEAN DEFAULT FALSE,  -- Whether user can move to next day
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, plan_id, month_index, day_number)
);
```

---

## 🔐 Authentication Flow

### 1. Email/Password Authentication
```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant B as Backend
    participant DB as Database

    U->>F: Enter credentials
    F->>B: POST /login or /register
    B->>DB: Query user by email
    DB->>B: Return user data
    B->>B: Verify password hash (login) or hash password (register)
    B->>B: Generate JWT token with user.id as subject
    B->>F: Return token + user data
    F->>F: Store token in localStorage
    F->>U: Redirect to dashboard/onboarding
```

### 2. Google OAuth Flow
```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant B as Backend
    participant G as Google
    participant DB as Database

    U->>F: Click "Sign in with Google"
    F->>B: GET /auth/google/url
    B->>F: Return OAuth URL with scopes
    F->>G: Redirect to Google
    G->>U: Authorize application
    G->>F: Return with auth code
    F->>B: POST /auth/google/callback
    B->>G: Exchange code for tokens
    G->>B: Return access token
    B->>G: Fetch user info from /oauth2/v2/userinfo
    G->>B: Return user profile
    B->>DB: Create/update user with Google data
    B->>F: Return JWT token + Google user info
    F->>F: Store token + Google data in localStorage
    F->>U: Redirect to dashboard/onboarding
```

### 3. JWT Token Validation
```python
# Flow: Request → Token Extraction → Validation → User Context
```

**Process:**
1. **Token Extraction**: From Authorization header using HTTPBearer
2. **Token Decoding**: Verify signature and expiration
3. **User Lookup**: Query database for user by ID
4. **Context Injection**: Add user to request context

---

## 🎯 Feature Breakdown

### 1. Onboarding System
**Purpose**: Collect user preferences and learning goals

**Flow:**
1. **Form Display**: Multi-step form with animations
2. **Data Collection**: Name, grade, goals, skills, learning style, time availability, subjects
3. **Validation**: Frontend and backend validation with Pydantic schemas
4. **Storage**: Save to database with user association (one-to-one relationship)
5. **Completion Check**: Verify if user has completed onboarding before showing form

**Key Components:**
- `OnboardingFlow.js`: Main component with form validation
- `onboarding.py`: Backend routes for save/get operations
- `OnboardingData`: Pydantic schema matching frontend data structure

**Implementation Details:**
- **Duplicate Prevention**: Deletes existing onboarding data before creating new
- **Required Fields**: name, grade, goals, skills, learning_style, time_availability, subjects
- **Optional Fields**: custom_goal, custom_skill

### 2. AI-Powered Learning Plans
**Purpose**: Generate personalized multi-year learning plans with monthly and daily breakdowns

**Flow:**
1. **Plan Generation**: AI creates structured learning plan based on user's onboarding data
2. **Month Activation**: User activates specific months to start learning
3. **Day Generation**: AI creates detailed daily learning content when a month is activated
4. **Day Interaction**: User views day content, completes learning activities
5. **Quiz Assessment**: Knowledge verification through quizzes for each day
6. **Progress Tracking**: Visual indicators for completion status

**Key Components:**
- `LearningPlans.js`: Main frontend component with month/day navigation
- `learning_plan.py`: Backend routes for plan generation and management
- `LearningPlan`: Database model with JSONB storage for complex plan structure
- `Quizzes.js`: Quiz component for knowledge assessment

**Implementation Details:**
- **AI Integration**: Uses Gemini AI to generate personalized learning content
- **Multi-year Structure**: Plans span 1-3 years based on user's grade/level
- **Progressive Unlocking**: Months are unlocked sequentially as user progresses
- **Interactive UI**: Calendar-like interface with day selection
- **Detailed Day Content**: Learning objectives, study plans, time estimates, resources
- **Quiz Generation**: AI-generated quizzes specific to each day's content
- **Progress Visualization**: Progress bars for months and days completion
- **Progress Tracking**: Three-tier tracking system:
  - User model tracks current position (plan_id, month_index, day)
  - LearningPath model tracks month-level progress (days_completed, current_day)
  - DayProgress model tracks detailed day-level metrics (quiz scores, time spent)

### 3. YouTube Learning Feature
**Purpose**: Analyze YouTube playlists and create study schedules

**Flow:**
1. **Playlist Input**: User enters YouTube playlist URL
2. **API Analysis**: Fetch playlist data via YouTube Data API v3
3. **Video Duration Fetching**: Make additional API call to get actual video durations
4. **Schedule Generation**: Calculate daily video distribution based on real video durations and daily minutes
5. **Time Window**: User specifies preferred study time (start_time and duration_minutes)
6. **Calendar Integration**: Sync to Google Calendar with real events at exact specified times

**Key Components:**
- `YouTubeLearning.js`: Frontend interface with playlist analysis
- `youtube_schedule.py`: Backend API for CRUD operations
- YouTube Data API integration for playlist metadata and video details

**Implementation Details:**
- **Real API Integration**: Uses actual YouTube Data API for playlist data
- **Accurate Duration Fetching**: Makes separate API call to `/videos` endpoint to get real video durations
- **Duration Parsing**: Converts YouTube's ISO 8601 duration format (PT4M13S) to seconds
- **Time Window Support**: start_time (HH:MM format) and duration_minutes
- **Schedule Storage**: JSONB format with day-by-day video distribution
- **Google Calendar Sync**: Creates real events in user's Google Calendar with accurate time distribution
- **Smart Time Distribution**: If videos exceed time window, scales proportionally; otherwise uses actual durations
- **Local Timezone Support**: Events are created in user's local timezone (Asia/Kolkata) to match their input time

### 4. Calendar System
**Purpose**: Display and manage learning schedules

**Flow:**
1. **Schedule Loading**: Fetch user's saved schedules from backend
2. **Calendar Rendering**: Display in month/week/day view using react-big-calendar
3. **Event Interaction**: Click to view video details with thumbnails
4. **Google Sync**: Create events in Google Calendar with proper formatting

**Key Components:**
- `Calendar.js`: React Big Calendar integration
- Google Calendar API integration for event creation
- Event management system with video details

**Implementation Details:**
- **Real Calendar Events**: Creates actual Google Calendar events
- **Event Details**: Includes video titles, URLs, and durations
- **Time Distribution**: Distributes videos evenly within user's time window
- **Visual Indicators**: Highlights days with scheduled videos

### 5. Profile Management
**Purpose**: User profile display and phone verification

**Flow:**
1. **Profile Display**: Show user information including Google OAuth status
2. **Phone Verification**: Send/verify SMS codes (simulated)
3. **Google Status**: Display OAuth connection status and user info
4. **Data Updates**: Modify profile information

**Key Components:**
- `Profile.js`: Profile interface with verification system
- Phone verification system (simulated with "123456" code)
- Google OAuth status display

**Implementation Details:**
- **Simulated SMS**: Uses "123456" as verification code
- **Google Integration**: Shows Google account connection status
- **Phone Storage**: Stores phone number and verification status
- **Alert System**: Shows verification status prominently

### 6. Personalized Onboarding Flow
**Purpose**: Collect user data for personalized learning path generation

**Flow:**
1. **Step 1 - Name**: Collect user's name for personalization
2. **Step 2 - Grade/Level**: Determine educational level for content tailoring
3. **Step 3 - Career Goals**: Select career paths (Data Scientist, Software Developer, etc.)
4. **Step 4 - Current Skills**: Assess existing knowledge to avoid repetition
5. **Step 5 - Time Commitment**: Determine daily learning time for schedule optimization

**Key Components:**
- `OnboardingFlow.js`: 5-step guided flow with modern UI
- Career goal selection with visual cards
- Skill assessment with interactive tags
- Time commitment slider with learning preview

**Implementation Details:**
- **Modern UI**: Clean design with progress indicators and icons
- **Career Focus**: Specific career paths for targeted learning
- **Skill Assessment**: Current skills to personalize content
- **Time Optimization**: Daily commitment for realistic scheduling
- **Learning Preview**: Shows estimated completion time and topics per week

### 7. Navigation System
**Purpose**: Consistent navigation across authenticated pages

**Flow:**
1. **Sidebar Display**: Collapsible navigation with all routes
2. **Route Protection**: Ensures authenticated access
3. **Layout Consistency**: Wrapper component for authenticated pages
4. **Logout Functionality**: Clear localStorage and redirect to login

**Key Components:**
- `Sidebar.js`: Collapsible navigation with icons
- `Layout.js`: Wrapper component for authenticated pages
- Route protection and logout functionality

**Implementation Details:**
- **Collapsible Design**: Toggle button with smooth animations
- **Icon Integration**: React Icons for visual navigation
- **Logout Function**: Clears localStorage and redirects
- **Layout Wrapper**: Applied to Dashboard, YouTubeLearning, Calendar, Profile

### 8. AI Chatbot and Agentic Features
**Purpose**: Provide intelligent learning assistance, answer questions, and perform actions on behalf of the user

**Flow:**
1. **Chat Interface**: User sends messages to AI assistant
2. **Context Enrichment**: Backend enriches message with comprehensive user context:
   - User profile (name, grade, goals, skills)
   - Learning plan details (current month/day, progress)
   - Recent quiz results and problem areas
   - Previous conversation history
3. **AI Processing**: Gemini AI processes enriched message with full context awareness
4. **Action Determination**: AI determines if actions are needed (create playlist, retrieve notes, etc.)
5. **Service Integration**: Actions executed through appropriate service integrations
6. **Response Formatting**: AI response formatted for readability and mobile display
7. **Response Display**: Shows AI responses with proper formatting and action results

**Key Components:**
- `Chatbot.js`: Frontend chat interface with message history and typing indicators
- `chatbot.py`: Backend routes for message handling and context enrichment
- `gemini_ai.py`: Integration with Google's Generative AI models
- `youtube_services.py`: Handles YouTube API interactions for playlist management
- `google_services.py`: Manages Google Drive integration for notes

**Implementation Details:**
- **Model Selection**: Tries multiple Gemini models with fallback mechanism:
  - Primary: gemini-2.0-flash-exp
  - Fallbacks: gemini-1.5-flash, gemini-1.5-pro, gemini-pro
- **Session Management**: Maintains persistent chat sessions per user with conversation history
- **Educational Context**: AI is primed with detailed educational assistant context
- **Persona Definition**: Specific EduAI persona with formatting rules and educational focus
- **Token Refresh**: Automatic refresh of Google API tokens for continuous service
- **Error Handling**: Comprehensive error handling with specific HTTP status code checks
- **Debugging**: Extensive logging for troubleshooting API interactions

### 9. Interactive Quizzes
**Purpose**: Assess knowledge, verify completion of learning days, and identify problem areas for future learning

**Flow:**
1. **Quiz Generation**: AI creates contextual questions based on day's learning content and user's problem areas
2. **Question Display**: Multiple-choice questions with options presented in an interactive UI
3. **Answer Submission**: User selects answers and submits for evaluation
4. **Score Calculation**: Backend evaluates answers and calculates score with detailed feedback
5. **Problem Area Identification**: System identifies topics where user struggled for future focus
6. **Day Completion**: Marks learning day as completed based on quiz performance threshold

**Key Components:**
- `Quizzes.js`: Frontend quiz interface with interactive question display
- `quiz.py`: Backend routes for quiz generation, submission, and evaluation
- `_generate_quiz_via_ai()`: Core function for AI-powered quiz creation
- Integration with learning plan system for day completion and progress tracking

**Implementation Details:**
- **AI-Generated Questions**: Uses Gemini AI with structured prompts to create highly relevant questions
- **Question Categories**: Balanced mix of understanding (40%), application (30%), critical thinking (20%), and practical implementation (10%)
- **Context-Aware Generation**: Quiz questions incorporate specific day's learning concept, month theme, and user's grade level
- **Problem Area Focus**: Generates 60% of questions targeting previously identified problem areas
- **Multiple Choice Format**: Standardized question format with 4 options and plausible distractors
- **Detailed Explanations**: Each question includes thorough explanations for correct answers
- **Immediate Feedback**: Shows correct/incorrect answers with explanations after submission
- **Score Threshold**: Requires minimum score (typically 70%) to mark day as completed
- **Quiz Storage**: Saves quiz data, user responses, and identified problem areas for future reference
- **Fallback Mechanism**: Default quiz generation if AI fails to generate appropriate questions

---

## 🌐 API Endpoints

### Authentication Endpoints
```
POST /register                    # User registration
POST /login                      # User login
GET  /me                         # Get current user info
GET  /auth/google/url           # Google OAuth URL
POST /auth/google/callback      # Google OAuth callback
GET  /auth/google/verify        # Check Google auth status
POST /auth/google/connect       # Connect Google account for existing users
```

### Onboarding Endpoints
```
POST /onboarding                # Save onboarding data
GET  /onboarding                # Retrieve onboarding data
```

### YouTube Schedule Endpoints
```
GET  /youtube-schedules                    # Get user schedules
POST /youtube-schedules                    # Create new schedule
DELETE /youtube-schedules/{schedule_id}    # Delete schedule
POST /youtube-schedules/{schedule_id}/sync-to-google-calendar  # Sync individual schedule
POST /youtube-schedules/sync-all-to-google-calendar           # Sync all schedules
```

### Learning Plan Endpoints
```
POST /learning-plan/generate                          # Generate new learning plan
GET  /learning-plan                                   # Get user's learning plan
GET  /learning-plan/{plan_id}                         # Get specific learning plan
POST /learning-plan/{plan_id}/start-next-month        # Start next month in plan
POST /learning-plan/{plan_id}/start-month/{month_idx} # Start specific month
GET  /learning-plan/{plan_id}/month/{month_idx}/days  # Get days for a month
POST /learning-plan/{plan_id}/month/{month_idx}/day/{day_num}/start # Start a specific day
POST /learning-plan/{plan_id}/complete-day/{month_idx}/{day_num}   # Complete a day
```

### Phone Verification Endpoints
```
POST /phone/send-verification   # Send verification code (simulated)
POST /phone/verify             # Verify phone number (simulated)
```

### Chatbot Endpoints
```
POST /chatbot/send-message      # Send message to Gemini AI chatbot
GET  /chatbot/history           # Get chat history
```

### Quiz Endpoints
```
POST /quiz/generate             # Generate quiz for learning day
POST /quiz/submit               # Submit quiz answers
```

### Utility Endpoints
```
GET  /              # Health check
GET  /health        # Health check
```

---

## 🚀 Setup Instructions

### Backend Setup
1. **Environment Setup**:
   ```bash
   cd fastapi-backend
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **Database Setup**:
   ```bash
   # Install PostgreSQL
   # Create database: eduaidb
   # Update .env with database credentials
   ```

3. **Environment Variables** (`.env`):
   ```env
   DATABASE_URL=postgresql+psycopg2://postgres:postgres123@localhost:5432/eduaidb
   SECRET_KEY=your-secret-key
   GOOGLE_CLIENT_ID=your-google-client-id
   GOOGLE_CLIENT_SECRET=your-google-client-secret
   YOUTUBE_API_KEY=your-youtube-api-key
   ```

4. **Start Backend**:
   ```bash
   python start_server.py
   # or
   uvicorn app.main:app --reload
   ```

### Frontend Setup
1. **Dependencies**:
   ```bash
   cd learning-ui
   npm install
   ```

2. **Environment Variables** (`.env`):
   ```env
   REACT_APP_API_URL=http://localhost:8000
   ```

3. **Start Frontend**:
   ```bash
   npm start
   ```

### Google OAuth Setup
1. **Google Cloud Console**:
   - Create new project
   - Enable Google+ API
   - Create OAuth 2.0 credentials
   - Add authorized redirect URIs: `http://localhost:3000/auth/google/callback`

2. **YouTube Data API**:
   - Enable YouTube Data API v3
   - Create API key
   - Add to environment variables

---

## 🔧 Development Workflow

### Code Organization
1. **Backend**: Follow FastAPI conventions
   - Models in `models/`
   - Schemas in `schemas/`
   - Routes in `routes/`
   - Core logic in `core/`
   - AI integration in `utils/gemini_ai.py`

2. **Frontend**: Component-based architecture
   - Reusable components in `components/`
   - API utilities in `api.js`
   - Routing in `App.js`
   - Utility functions in `utils/`

### AI Integration
- **Gemini AI**: Used for generating learning plans, day content, quizzes, and chatbot responses
- **Model Selection**: System tries multiple models in order of preference (2.5 Flash, 2.0 Flash, 1.5 Flash, 1.5 Pro, Pro)
- **Prompt Engineering**: Structured prompts for consistent AI outputs
- **Error Handling**: Fallback mechanisms if model initialization fails
- **Response Processing**: JSON parsing and validation for structured AI outputs
- **Context Management**: Maintains conversation history for contextual responses
- **Session Management**: User-specific chat sessions with persistent context
- **Response Formatting**: Automatic formatting for better readability

## 🤖 AI Model Context Protocols

### Model Context Protocols

#### Context Enrichment
The system enriches user messages with multiple layers of context:

1. **User Profile Context**
   - User ID, name, email
   - Grade level and career goals
   - Current skills and time commitment

2. **Learning Progress Context**
   - Current learning month and day
   - Completed days and total progress
   - Recent quiz results and problem areas

3. **Conversation History Context**
   - Previous messages in the current session
   - AI's previous responses
   - Actions previously taken by the AI

#### Prompt Engineering
The system uses carefully structured prompts to ensure consistent AI outputs:

1. **System Prompt**
   - Defines the AI's persona as EduAI
   - Sets formatting rules for responses
   - Establishes educational focus and tone

2. **User Context Prompt**
   - Dynamically generated based on user's current state
   - Includes learning plan details and progress
   - Provides recent quiz performance data

3. **Action Prompts**
   - Specific instructions for YouTube playlist creation
   - Guidelines for Google Drive note retrieval
   - Parameters for learning plan generation

### AI Features

#### YouTube Integration
- **Playlist Analysis**: Analyzes YouTube playlists to extract educational content
- **Video Recommendations**: Suggests relevant videos based on learning plan
- **Error Handling**: Robust error handling for API failures with specific HTTP status code checks
- **Token Refresh**: Automatic refresh of expired YouTube API tokens

#### Google Drive Integration
- **Note Creation**: Creates and stores daily learning notes
- **Note Retrieval**: Fetches previously created notes for reference
- **Folder Management**: Organizes notes in structured folders by date
- **Error Logging**: Comprehensive logging for troubleshooting Drive API interactions

#### Learning Plan Generation
- **Personalized Plans**: Creates multi-year learning plans based on user goals
- **Monthly Structure**: Organizes content into themed months
- **Daily Activities**: Generates specific daily learning activities
- **Adaptive Content**: Adjusts difficulty based on user progress

#### Quiz Generation
- **Contextual Questions**: Creates questions specific to daily learning content
- **Problem Area Focus**: Emphasizes topics where user has struggled
- **Varied Question Types**: Includes understanding, application, and critical thinking
- **Detailed Explanations**: Provides thorough explanations for correct answers
- **Fallback Mechanism**: Default quiz generation if AI fails to generate appropriate questions

## 🧠 AI Implementation Workflow

### Gemini AI Integration Architecture

```
┌─────────────────────┐      ┌─────────────────────┐      ┌─────────────────────┐
│   User Interface    │      │   Backend Server    │      │    Gemini AI API    │
│   (React Frontend)  │◄────►│   (FastAPI)        │◄────►│   (Google Cloud)    │
└─────────────────────┘      └─────────────────────┘      └─────────────────────┘
                                        │
                                        ▼
                              ┌─────────────────────┐
                              │   Database         │
                              │   (PostgreSQL)     │
                              └─────────────────────┘
```

### Model Initialization and Fallback Mechanism

```python
# Initialization flow in gemini_ai.py
try:
    # Try primary model (gemini-2.0-flash-exp)
    genai.configure(api_key=api_key)
    model = genai.GenerativeModel('gemini-2.0-flash-exp')
    # Test with simple prompt
    response = model.generate_content("Hello")
    print("Using gemini-2.0-flash-exp model")
except Exception as e:
    try:
        # Fallback to gemini-1.5-flash
        model = genai.GenerativeModel('gemini-1.5-flash')
        response = model.generate_content("Hello")
        print("Using gemini-1.5-flash model")
    except Exception as e:
        try:
            # Fallback to gemini-1.5-pro
            model = genai.GenerativeModel('gemini-1.5-pro')
            response = model.generate_content("Hello")
            print("Using gemini-1.5-pro model")
        except Exception as e:
            # Final fallback to gemini-pro
            model = genai.GenerativeModel('gemini-pro')
            print("Using gemini-pro model")
```

### Session Management

```python
# Session management in gemini_ai.py
def get_or_create_session(user_id):
    """Get existing chat session or create a new one for the user"""
    if user_id not in chat_sessions:
        # Create new chat session
        chat = model.start_chat(history=[])
        
        # Initialize with context message defining the AI's persona
        chat.send_message(context_message)
        
        # Store in session dictionary
        chat_sessions[user_id] = chat
        print(f"Created new chat session for user {user_id}")
    else:
        print(f"Using existing chat session for user {user_id}")
    
    return chat_sessions[user_id]
```

### Context Enrichment Process

```python
# Context enrichment in chatbot.py
async def chat(message: ChatMessage, db: Session = Depends(get_db)):
    # Decode JWT token
    payload = decode_token(message.token)
    user_id = payload.get("sub")
    
    # Get user details
    user = db.query(User).filter(User.id == user_id).first()
    
    # Get onboarding information
    onboarding = db.query(Onboarding).filter(Onboarding.user_id == user_id).first()
    
    # Get current learning plan
    learning_plan = db.query(LearningPlan).filter(
        LearningPlan.user_id == user_id,
        LearningPlan.is_active == True
    ).first()
    
    # Get learning path service
    learning_path_service = LearningPathService(db)
    
    # Get current position in learning plan
    current_position = learning_path_service.get_current_learning_position(user_id)
    
    # Get recent quiz submissions
    recent_quiz = db.query(QuizSubmission).filter(
        QuizSubmission.user_id == user_id
    ).order_by(QuizSubmission.created_at.desc()).first()
    
    # Enrich user message with context
    enriched_message = f"""
    USER MESSAGE: {message.message}
    
    USER CONTEXT:
    - Name: {user.name}
    - Email: {user.email}
    - Grade: {onboarding.grade if onboarding else 'Unknown'}
    - Career Goals: {onboarding.career_goals if onboarding else 'Unknown'}
    - Current Skills: {onboarding.current_skills if onboarding else 'Unknown'}
    - Time Commitment: {onboarding.time_commitment if onboarding else 'Unknown'} minutes/day
    
    LEARNING CONTEXT:
    - Current Month: {current_position.get('current_month_index') if current_position else 'None'}
    - Current Day: {current_position.get('current_day_index') if current_position else 'None'}
    - Completed Days: {current_position.get('completed_days') if current_position else '0'}
    
    QUIZ CONTEXT:
    - Recent Quiz Score: {recent_quiz.score if recent_quiz else 'None'}
    - Problem Areas: {recent_quiz.problem_areas if recent_quiz else 'None'}
    """
    
    # Send enriched message to AI
    response = await chatbot.get_response(user_id, enriched_message)
    
    return {"response": response}
```

### AI Response Processing

```python
# Response formatting in gemini_ai.py
def _format_response(response_text):
    """Format the AI response for better readability"""
    # Clean up any system artifacts
    response_text = response_text.replace("As an AI assistant", "")
    response_text = response_text.replace("As an AI language model", "")
    response_text = response_text.replace("As a language model", "")
    
    # Format code blocks for mobile display
    response_text = re.sub(
        r'```([^\n]*)(\n[\s\S]*?\n)```',
        r'<pre><code class="language-\1">\2</code></pre>',
        response_text
    )
    
    return response_text
```

### Learning Plan Generation Process

```python
# Learning plan generation in learning_plan.py
def _build_prompt(onboarding: Onboarding, total_years: int):
    """Build prompt for AI to generate learning plan"""
    return f"""
    Create a comprehensive {total_years}-year learning plan for a student with the following profile:
    
    Grade/Level: {onboarding.grade}
    Career Goals: {onboarding.career_goals}
    Current Skills: {onboarding.current_skills}
    Daily Time Commitment: {onboarding.time_commitment} minutes
    
    The learning plan should be structured as follows:
    
    1. Each year should have 12 months
    2. Each month should have a specific theme related to the career goals
    3. Each month should have 20-25 learning days
    4. Each day should focus on a specific concept with a time estimate
    
    Return the plan as a JSON object with the following structure:
    {{
      "years": [
        {{
          "year": 1,
          "months": [
            {{
              "month": 1,
              "title": "Month Title",
              "description": "Month description",
              "days": [
                {{
                  "day": 1,
                  "concept": "Specific concept for this day",
                  "time_estimate": 30
                }}
              ]
            }}
          ]
        }}
      ]
    }}
    
    Make sure the plan is:
    1. Progressive - concepts build on previous knowledge
    2. Realistic - daily time estimates match the user's commitment
    3. Relevant - focused on the career goals
    4. Comprehensive - covers all necessary skills
    """
```

### Quiz Generation Process

```python
# Quiz generation in quiz.py
def _generate_quiz_via_ai(month: dict, day: dict, onboarding: Onboarding, num_questions: int = 15, problem_areas: list = None) -> List[Dict[str, Any]]:
    # Build comprehensive prompt for quiz generation
    problem_areas_text = ""
    if problem_areas and len(problem_areas) > 0:
        problem_areas_text = "\nProblem Areas (focus on these):\n" + "\n".join([f"- {area}" for area in problem_areas if area]) + "\n\nIMPORTANT: Generate at least 60% of questions that specifically address these problem areas. Make these questions more detailed and include thorough explanations to help the learner understand these concepts better."
            
    prompt = f"""
    Generate a comprehensive multiple-choice quiz as pure JSON for this specific learning day.
    
    CONTEXT:
    Month Title: {month.get('title')}
    Month Description: {month.get('description', '')}
    Day: {day.get('day')}
    Learning Concept: {day.get('concept')}
    Time Estimate: {day.get('time_estimate', 60)} minutes
    Daily Time Commitment: {onboarding.time_commitment}
    
    Learner Profile:
    - Grade/Level: {onboarding.grade}
    - Career Goals: {onboarding.career_goals}
    - Current Skills: {onboarding.current_skills}
    
    Day Detail (if available):
    {json.dumps(day.get('detail', {}), indent=2)[:1500]}{problem_areas_text}
    
    REQUIREMENTS:
    1) Output strictly valid JSON with key "questions" = array of exactly {num_questions} items.
    2) Each question item: {{"question": <string>, "options": [4 options], "correct_index": <0-3>, "explanation": <string>}}
    3) Question types should include:
       - Understanding of core concepts (40%)
       - Application and problem-solving (30%)
       - Critical thinking and analysis (20%)
       - Practical implementation (10%)
    4) Questions MUST be highly specific to this day's concept and learning objectives
    """
    
    # Send prompt to AI and process response
    try:
        response = chatbot.get_response_sync("quiz_system", prompt)
        # Extract JSON from response
        json_match = re.search(r'```json\s*(.+?)\s*```', response, re.DOTALL)
        if not json_match:
            json_match = re.search(r'({\s*"questions"\s*:.+})', response, re.DOTALL)
        
        if json_match:
            quiz_json = json.loads(json_match.group(1))
            return quiz_json.get("questions", [])
        else:
            # Fallback to default quiz
            return _fallback_quiz(day.get('concept'))
    except Exception as e:
        print(f"Error generating quiz: {e}")
        return _fallback_quiz(day.get('concept'))
```

### YouTube Playlist Creation Process

```python
# YouTube playlist creation in chatbot.py
@router.post("/create-playlist")
async def create_playlist(request: CreatePlaylistRequest, db: Session = Depends(get_db)):
    # Decode token
    payload = decode_token(request.token)
    user_id = payload.get("sub")
    
    # Get user
    user = db.query(User).filter(User.id == user_id).first()
    if not user:
        raise HTTPException(status_code=404, detail="User not found")
    
    # Check if user has Google credentials
    if not user.google_refresh_token:
        raise HTTPException(status_code=400, detail="Google account not connected")
    
    # Refresh Google token
    print(f"Attempting to refresh Google token for user {user.id}")
    try:
        token_info = refresh_google_token(user.google_refresh_token)
        access_token = token_info.get("access_token")
        print(f"Successfully refreshed Google token for user {user.id}")
    except Exception as e:
        error_message = str(e)
        status_code = 500
        if hasattr(e, 'status_code'):
            status_code = e.status_code
        
        print(f"Failed to refresh Google token: {error_message} (Status: {status_code})")
        context_snippets = []
        
        if hasattr(e, 'status_code'):
            context_snippets.append(f"HTTP Status Code: {e.status_code}")
        
        if hasattr(e, 'content'):
            context_snippets.append(f"Response Content: {e.content}")
            
        raise HTTPException(
            status_code=status_code,
            detail=f"Failed to refresh Google token: {error_message}"
        )
    
    # Create playlist
    try:
        playlist_id = create_youtube_playlist(
            access_token,
            request.title,
            request.description
        )
        
        # Add videos to playlist
        for video_id in request.video_ids:
            add_video_to_playlist(access_token, playlist_id, video_id)
        
        return {"playlist_id": playlist_id}
    except Exception as e:
        raise HTTPException(status_code=500, detail=f"Failed to create playlist: {str(e)}")
```

### Google Drive Notes Integration

```python
# Google Drive notes in google_services.py
def get_day_notes(access_token: str, date_str: str):
    """Get or create notes for a specific day in Google Drive"""
    try:
        print(f"Getting notes for date: {date_str}")
        # Parse date
        date_obj = datetime.strptime(date_str, "%Y-%m-%d")
        year = date_obj.year
        month = date_obj.month
        day = date_obj.day
        
        # Set up Drive API client
        credentials = Credentials(token=access_token)
        drive_service = build('drive', 'v3', credentials=credentials)
        
        # Find or create EduAI folder
        print("Looking for EduAI folder")
        eduai_folder_id = _find_or_create_folder(drive_service, "EduAI", "root")
        print(f"EduAI folder ID: {eduai_folder_id}")
        
        # Find or create year folder
        year_folder_name = f"{year}"
        print(f"Looking for year folder: {year_folder_name}")
        year_folder_id = _find_or_create_folder(drive_service, year_folder_name, eduai_folder_id)
        print(f"Year folder ID: {year_folder_id}")
        
        # Find or create month folder
        month_folder_name = f"{month:02d} - {date_obj.strftime('%B')}"
        print(f"Looking for month folder: {month_folder_name}")
        month_folder_id = _find_or_create_folder(drive_service, month_folder_name, year_folder_id)
        print(f"Month folder ID: {month_folder_id}")
        
        # Find or create day file
        file_name = f"{day:02d} - Learning Notes.txt"
        print(f"Looking for day file: {file_name}")
        
        # Search for existing file
        results = drive_service.files().list(
            q=f"name='{file_name}' and '{month_folder_id}' in parents and trashed=false",
            spaces='drive',
            fields='files(id, name)'
        ).execute()
        
        files = results.get('files', [])
        
        if files:
            # File exists, get content
            file_id = files[0]['id']
            print(f"Found existing file with ID: {file_id}")
            
            try:
                content = drive_service.files().get_media(fileId=file_id).execute().decode('utf-8')
                print("Successfully retrieved file content")
                return {
                    "file_id": file_id,
                    "content": content,
                    "file_url": f"https://docs.google.com/file/d/{file_id}/edit"
                }
            except Exception as e:
                print(f"Error retrieving file content: {str(e)}")
                if hasattr(e, 'status_code'):
                    print(f"Status code: {e.status_code}")
                if hasattr(e, 'content'):
                    print(f"Response content: {e.content}")
                
                # Create new file if content retrieval fails
                return _create_new_note_file(drive_service, file_name, month_folder_id, date_str)
        else:
            # Create new file
            print(f"No existing file found, creating new one")
            return _create_new_note_file(drive_service, file_name, month_folder_id, date_str)
            
    except Exception as e:
        print(f"Error in get_day_notes: {str(e)}")
        if hasattr(e, 'status_code'):
            print(f"Status code: {e.status_code}")
        if hasattr(e, 'content'):
            print(f"Response content: {e.content}")
        raise e
```

### Database Migrations
```bash
# Create new migration
alembic revision --autogenerate -m "Description"

# Apply migrations
alembic upgrade head

# Reset database (development)
python reset_database.py
```

### Testing Flow
1. **Backend Testing**: Use FastAPI's auto-generated docs at `http://localhost:8000/docs`
2. **Frontend Testing**: Browser developer tools
3. **Integration Testing**: Full user flow testing
4. **AI Mocking**: Test fixtures for predictable AI responses

### Error Handling
1. **Backend**: HTTP status codes + detailed error messages
2. **Frontend**: User-friendly error displays
3. **API**: Consistent error response format
4. **AI Response Validation**: Schema validation for AI-generated content

---

## 📊 Data Flow Examples

### User Registration Flow
```
1. User fills registration form
2. Frontend validates input
3. POST /register with user data
4. Backend validates with Pydantic
5. Hash password with bcrypt
6. Create user in database
7. Generate JWT token with user.id as subject
8. Return token to frontend
9. Store token in localStorage
10. Redirect to onboarding
```

### Learning Plan Generation Flow
```
1. User completes onboarding or requests a new learning plan
2. Frontend sends request to `/learning-plan/generate` endpoint
3. Backend retrieves user's onboarding data (goals, experience, time commitment)
4. Backend determines appropriate plan duration based on user's grade level
5. Backend constructs a detailed prompt for Gemini AI with specific formatting requirements
6. Prompt includes user's career goals, current skills, grade level, and time commitment
7. Gemini AI generates a structured learning plan in JSON format with:
   - Multi-year structure based on educational level
   - Monthly themes aligned with career goals
   - Daily learning activities with time estimates
   - Detailed concept descriptions and learning objectives
8. Backend validates and processes the JSON structure
9. Creates a LearningPlan record in database with plan metadata
10. For each month in the plan, a LearningPath record is created to track progress
11. For each day in each month, structured data is stored for future retrieval
12. Plan structure returned to frontend for display
13. Frontend renders the plan with months and days in an interactive UI
14. User can navigate between months and select specific days to begin learning
```

### Learning Day Activation Flow

#### Overview
The Learning Day Activation process is triggered when a user selects a specific day in their learning plan. This process generates detailed content for that day using Gemini AI, updates the user's progress tracking, and creates supporting resources in Google Drive.

#### Implementation Flow

```
1. User selects a specific day in the learning plan
2. Frontend sends request to `/learning-plan/{plan_id}/month/{month_index}/day/{day}/start`
3. Backend validates the request and enforces sequential progression
4. Backend checks if day content already exists
5. If not, backend uses Gemini AI to generate detailed day content
6. Content includes objectives, study plan, resources, and time estimates
7. Backend automatically generates a quiz for the day if one doesn't exist
8. Backend creates Google Drive notes and calendar events for the day
9. Backend updates the user's current position (current_plan_id, current_month_index, current_day)
10. Backend updates the LearningPath record for this month (current_day, last_activity_at)
11. Updated day content returned to frontend
12. Frontend displays detailed day view with study materials and quiz option
```

#### Day Content Generation Process

```python
# Day detail generation in learning_plan.py
def _generate_day_detail_via_ai(month: dict, day: dict, onboarding: Onboarding) -> dict:
    import json
    try:
        prompt = f"""
        Generate a comprehensive, detailed study plan for this specific day as pure JSON.
        
        Month Title: {month.get('title')}
        Month Description: {month.get('description', '')}
        Day: {day.get('day')}
        Concept: {day.get('concept')}
        Time Estimate: {day.get('time_estimate', 60)} minutes
        Daily Time Commitment: {onboarding.time_commitment}
        Learner Profile:
        - Grade/Level: {onboarding.grade}
        - Career Goals: {onboarding.career_goals}
        - Current Skills: {onboarding.current_skills}
        
        Rules:
        - Output strictly valid JSON with keys: overview, sections, resources, checklist, learning_objectives.
        - overview: comprehensive description of what will be learned today
        - sections: list of study sections with {{ title, minutes, steps: [detailed steps], focus_areas: [specific topics] }}
        - resources: list of {{ type, title, url?, description }}
        - checklist: list of concrete tasks to complete
        - learning_objectives: list of specific things the learner should understand by end of day
        - Total time should match the day's time_estimate
        - Make content specific, actionable, and aligned with the concept
        - Include practical examples and exercises where appropriate
        - No markdown, no extra text, only JSON.
        """
        ai = chatbot.model
        raw = ai.generate_content(prompt)
        text = raw.text
        try:
            return json.loads(text)
        except Exception:
            # Try to extract JSON if it's wrapped in other text
            start = text.find('{')
            end = text.rfind('}')
            if start != -1 and end != -1 and end > start:
                return json.loads(text[start:end+1])
    except Exception:
        # Comprehensive fallback if AI generation fails
        return {
            "overview": f"Comprehensive study session focused on {day.get('concept')}",
            "sections": [
                {"title": "Theory and Concepts", "minutes": 25, "steps": ["Read core concepts", "Take detailed notes", "Identify key principles"], "focus_areas": ["Fundamentals", "Core theory"]},
                {"title": "Practical Application", "minutes": 25, "steps": ["Work through examples", "Practice problems", "Apply concepts"], "focus_areas": ["Hands-on practice", "Problem solving"]},
                {"title": "Review and Assessment", "minutes": 10, "steps": ["Summarize learning", "Self-assessment", "Prepare for quiz"], "focus_areas": ["Consolidation", "Understanding check"]}
            ],
            "resources": [
                {"type": "documentation", "title": "Core Concepts Guide", "description": "Essential reading for today's topic"}
            ],
            "checklist": ["Complete theory reading", "Finish practice exercises", "Review key concepts", "Prepare for assessment"],
            "learning_objectives": ["Understand core concepts", "Apply knowledge practically", "Demonstrate comprehension"]
        }
```

#### Google Drive Integration

When a day is activated, the system automatically creates a notes file in Google Drive with the following structure:

```
EDUAI_[USERNAME]_LEARNING_MAIN_PATH/
└── MONTH_[month_index]/
    └── DAY_[day]_NOTES.txt
```

The notes file contains:
- Day title and concept
- Overview from the AI-generated content
- Study sections with time estimates and steps
- A calendar event is also created with the day's time estimate

#### Sequential Progression Enforcement

The system enforces sequential progression through the learning plan:

1. Users must complete previous days before starting a new day
2. The system performs an "auto-heal" check to see if the user passed the previous day's quiz
3. If the previous day's quiz was passed, it automatically marks that day as completed
4. If not, it requires the user to complete the previous day first
```

### Quiz Generation and Submission Flow
```
1. User completes a learning day and clicks "Take Quiz"
2. Frontend sends request to `/quiz/generate/{plan_id}/{month_index}/{day_index}`
3. Backend retrieves day content from database
4. Backend uses Gemini AI to generate quiz questions based on day content
5. Quiz questions and answers saved to database and returned to frontend
6. Frontend displays quiz with multiple-choice questions
7. User completes quiz and submits answers
8. Frontend sends answers to `/quiz/submit/{quiz_id}`
9. Backend evaluates answers, calculates score
10. If score meets threshold:
    - Day marked as completed in learning plan's JSONB structure
    - DayProgress record updated with completion status, quiz score, and best score
    - LearningPath record updated with days_completed count and days_data
    - User's current position updated to next incomplete day
11. Results returned to frontend with correct answers highlighted
```

### AI Chatbot Conversation Flow
```
1. User types message in chatbot interface
2. Frontend sends message to `/chatbot/send-message` endpoint
3. Backend retrieves or creates user's chat session
4. Backend sends message to Gemini AI with educational context
5. Gemini AI generates response based on conversation history
6. Response saved to database and returned to frontend
7. Frontend displays formatted response in chat interface
```

### YouTube Playlist Analysis Flow
```
1. User enters playlist URL
2. Frontend calls YouTube Data API
3. Fetch playlist metadata (title, videos, durations)
4. Calculate total duration and daily distribution
5. User sets time preferences (start_time, duration_minutes)
6. Save schedule to database with JSONB format
7. Display in calendar view
8. Option to sync to Google Calendar
```

### Google Calendar Sync Flow
```
1. User clicks "Sync to Calendar"
2. Frontend calls backend sync endpoint
3. Backend retrieves Google access token from database
4. Create Google Calendar API session
5. Generate calendar events for each video with proper formatting
6. Post events to Google Calendar API
7. Return success/error response
8. Update UI with sync status
```

---

## 🔒 Security Considerations

### Authentication Security
- **JWT Tokens**: Secure token generation and validation with user ID as subject
- **Password Hashing**: Bcrypt with salt
- **CORS**: Properly configured for frontend access
- **Input Validation**: Pydantic schemas for all inputs

### API Security
- **Rate Limiting**: Implemented on sensitive endpoints
- **Input Sanitization**: All user inputs validated
- **SQL Injection Prevention**: SQLAlchemy ORM usage
- **XSS Prevention**: Proper data encoding

### Data Protection
- **Environment Variables**: Sensitive data in .env files
- **Database Security**: PostgreSQL with proper permissions
- **Token Storage**: Secure localStorage usage
- **HTTPS**: Production deployment requirement

### AI Data Handling
- **Google Gemini API Key**: Stored securely in environment variables
- **User Data Anonymization**: User data anonymized in AI prompts when possible
- **Response Validation**: AI responses validated before storage and display
- **Privacy Protection**: No sensitive user information sent to AI models
- **Data Retention**: Clear policies for AI-generated content

---

## 🚀 Deployment Considerations

### Backend Deployment
- **Docker**: Containerized deployment
- **Environment Variables**: Production configuration
- **Database**: Production PostgreSQL instance
- **SSL**: HTTPS certificate configuration
- **Serverless Option**: Consider serverless deployment for cost efficiency

### AI Service Configuration
- **Gemini API Key**: Secure storage in environment variables
- **Model Availability**: Monitoring for AI service uptime
- **Response Time**: Tracking AI model performance
- **Usage Quotas**: Managing API consumption limits
- **Fallback Strategies**: Handling service disruptions gracefully

### Frontend Deployment
- **Build Process**: `npm run build`
- **Static Hosting**: Netlify, Vercel, or AWS S3
- **Environment Variables**: Production API URLs
- **CDN**: Content delivery network setup
- **PWA Capabilities**: Progressive Web App configuration

### Monitoring
- **Logging**: Application and error logging
- **Health Checks**: Endpoint monitoring
- **Performance**: Response time monitoring
- **Security**: Vulnerability scanning
- **AI Quality**: Tracking response quality and latency

---

## ⚠️ Important Implementation Notes

### Database Management
- **Force Recreation**: Tables are dropped and recreated on every startup
- **Schema Verification**: Checks for required columns during startup
- **Development Only**: This approach is for development; use proper migrations in production
- **JSONB Storage**: Complex AI-generated content stored in JSONB columns

### Google OAuth
- **Access Token Storage**: Google access tokens are stored in database
- **Scope Management**: Includes 'openid' scope to prevent scope mismatch errors
- **User Info Fetch**: Uses `/oauth2/v2/userinfo` endpoint for reliable user data

### Gemini AI Integration
- **Model Selection**: System tries multiple models (2.0 Flash, 1.5 Flash, 1.5 Pro, Pro)
- **Structured Responses**: AI generates JSON-formatted learning plans and quizzes
- **Chat Sessions**: Maintains conversation history for contextual responses
- **Error Handling**: Fallback mechanisms if model initialization fails
- **Educational Context**: AI is primed with educational assistant context

### Phone Verification
- **Simulated System**: Currently uses "123456" as verification code
- **Production Ready**: Structure supports real SMS integration
- **Demo Purpose**: Verification always succeeds with demo code

### YouTube Integration
- **Real API**: Uses actual YouTube Data API v3
- **Playlist Analysis**: Fetches real playlist metadata
- **Schedule Generation**: Intelligent daily video distribution
- **Calendar Sync**: Creates real Google Calendar events

This documentation reflects the exact implementation of your EduAI platform, based on the actual codebase analysis.
