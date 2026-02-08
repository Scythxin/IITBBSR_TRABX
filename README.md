# IITBBSR_TRABX
# 🌌 IITBBSR TRABX - Asteroid Tracking and Risk Assessment System

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-0.68+-green.svg)
![NASA API](https://img.shields.io/badge/NASA-NEO%20API-red.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

A comprehensive web-based asteroid tracking and risk assessment system that integrates with NASA's Near-Earth Object (NEO) API to monitor, analyze, and alert users about potentially hazardous asteroids approaching Earth.

## 📋 Table of Contents

- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Architecture](#-architecture)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Usage](#-usage)
- [API Endpoints](#-api-endpoints)
- [Risk Calculation](#-risk-calculation)
- [Database Schema](#-database-schema)
- [Project Structure](#-project-structure)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)

## ✨ Features

### 🔐 User Authentication
- User registration and login system
- Session management
- Secure password storage

### 🌍 3D Planetary Visualization
- Interactive 3D solar system visualization using Three.js
- High-quality planet textures
- Real-time rotation and orbital mechanics
- Zoom and pan controls

### 🔍 Asteroid Search & Tracking
- Search asteroids by date range
- Real-time data fetching from NASA's NEO API
- Detailed asteroid information including:
  - Name and NEO ID
  - Diameter (km)
  - Velocity (km/s)
  - Miss distance (km)
  - Hazard classification

### ⚠️ Risk Assessment System
- Automated risk score calculation
- Four-tier risk classification:
  - 🔴 **CRITICAL** (Score ≥ 80)
  - 🟠 **HIGH** (Score ≥ 50)
  - 🟡 **MODERATE** (Score ≥ 30)
  - 🟢 **LOW** (Score < 30)
- Persistent risk data storage
- Alert system for high-risk asteroids

### 💬 Community Chat
- Real-time WebSocket-based chat
- Message persistence
- Chat history retrieval
- Multi-user support

### 📊 Data Management
- Bulk asteroid data import from NASA
- Duplicate detection and handling
- Data statistics and reporting

## 🛠 Technology Stack

### Backend
- **FastAPI** - Modern, fast web framework for building APIs
- **SQLAlchemy** - SQL toolkit and ORM
- **SQLite** - Lightweight database
- **WebSockets** - Real-time bidirectional communication
- **Requests** - HTTP library for NASA API integration

### Frontend
- **HTML5/CSS3** - Modern web standards
- **JavaScript** - Client-side scripting
- **Three.js** - 3D graphics library for planetary visualization
- **Jinja2** - Template engine

### External APIs
- **NASA NEO (Near-Earth Object) API** - Asteroid data source

## 🏗 Architecture

```
┌─────────────────┐
│   Web Browser   │
│  (User Client)  │
└────────┬────────┘
         │
         ├─── HTTP/HTTPS ───┐
         │                  │
         ├─── WebSocket ────┤
         │                  │
         ▼                  ▼
┌─────────────────────────────┐
│      FastAPI Server         │
│  ┌─────────────────────┐   │
│  │   Authentication    │   │
│  ├─────────────────────┤   │
│  │   Route Handlers    │   │
│  ├─────────────────────┤   │
│  │   Risk Calculator   │   │
│  ├─────────────────────┤   │
│  │  WebSocket Manager  │   │
│  └─────────────────────┘   │
└──────────┬──────────────────┘
           │
           ├─── SQLAlchemy ORM
           │
           ▼
    ┌─────────────┐
    │   SQLite    │
    │  Database   │
    └─────────────┘
           │
           ├─── HTTP Requests
           │
           ▼
    ┌─────────────┐
    │  NASA NEO   │
    │     API     │
    └─────────────┘
```

## 📦 Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Git

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/IITBBSR_TRABX.git
cd IITBBSR_TRABX
```

### Step 2: Create Virtual Environment (Recommended)
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Initialize Database
The database will be automatically created when you first run the application.

### Step 5: Run the Application
```bash
uvicorn main:app --reload
```

The application will be available at: `http://localhost:8000`

**Note:** For production use, it's recommended to:
1. Get your own API key from [NASA API Portal](https://api.nasa.gov/)
2. Store it in environment variables
3. Update the configuration accordingly

### Environment Variables (Optional)
Create a `.env` file in the project root:

```env
NASA_API_KEY=your_api_key_here
DATABASE_URL=sqlite:///./users.db
SECRET_KEY=your_secret_key_here
```

## 🚀 Usage

### 1. User Registration & Login
1. Navigate to `http://localhost:8000`
2. Click "Register" to create a new account
3. Enter username and password
4. Login with your credentials

### 2. Viewing the Dashboard
After login, you'll see the main dashboard with:
- 3D planetary system visualization
- Navigation to different features

### 3. Searching Asteroids by Date
1. Click "Search Asteroids"
2. Select a date
3. Click "Search"
4. View results with risk assessments

### 4. Fetching NASA Data
```bash
# Using curl or browser
GET http://localhost:8000/nasa/neo/save?start_date=2024-01-01&end_date=2024-01-07
```

### 5. Viewing Risk Alerts
1. Navigate to "Alerts" page
2. View list of HIGH and CRITICAL risk asteroids
3. Sorted by risk score

### 6. Community Chat
1. Click "Chat" in the navigation
2. View message history
3. Send messages to other users in real-time

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/register` | Register new user |
| POST | `/login` | User login |

### Pages
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Landing/Auth page |
| GET | `/dashboard` | Main dashboard |
| GET | `/alerts` | Alerts page |
| GET | `/chat` | Chat page |
| GET | `/asteroids/search` | Asteroid search page |

### NASA Data
| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| GET | `/nasa/neo/save` | Fetch and save NASA data | `start_date`, `end_date` |
| GET | `/api/asteroids/by-date` | Get asteroids by date | `date` |

### Risk Assessment
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/asteroids/risk` | Calculate risk for all asteroids |
| POST | `/asteroids/risk/save` | Save risk assessments to DB |
| GET | `/asteroids/alerts` | Get HIGH/CRITICAL alerts |

### Chat
| Method | Endpoint | Description |
|--------|----------|-------------|
| WebSocket | `/ws/chat` | Real-time chat connection |
| GET | `/chat/history` | Get chat history |

## 🎯 Risk Calculation

The risk score is calculated using the following formula:

```python
risk_score = (diameter_km × 40) + 
             (velocity_km_s × 2) - 
             (miss_distance_km ÷ 1,000,000) +
             (hazardous_bonus)
```

Where:
- `diameter_km`: Asteroid diameter in kilometers
- `velocity_km_s`: Relative velocity in km/s
- `miss_distance_km`: Miss distance in kilometers
- `hazardous_bonus`: +30 points if NASA classifies as potentially hazardous

### Risk Levels
- **CRITICAL**: Score ≥ 80 (Immediate attention required)
- **HIGH**: Score ≥ 50 (Close monitoring needed)
- **MODERATE**: Score ≥ 30 (Standard tracking)
- **LOW**: Score < 30 (Minimal concern)

## 🗄 Database Schema

### Users Table
```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    username VARCHAR UNIQUE NOT NULL,
    password VARCHAR NOT NULL
);
```

### Asteroids Table
```sql
CREATE TABLE asteroids (
    id INTEGER PRIMARY KEY,
    neo_id VARCHAR UNIQUE NOT NULL,
    name VARCHAR,
    close_approach_date VARCHAR,
    diameter_km FLOAT,
    velocity_km_s FLOAT,
    hazardous BOOLEAN,
    nasa_url VARCHAR
);
```

### AsteroidRisk Table
```sql
CREATE TABLE asteroid_risk (
    id INTEGER PRIMARY KEY,
    neo_id VARCHAR,
    name VARCHAR,
    close_approach_date VARCHAR,
    diameter_km FLOAT,
    velocity_km_s FLOAT,
    hazardous BOOLEAN,
    risk_score FLOAT,
    risk_level VARCHAR
);
```

### ChatMessages Table
```sql
CREATE TABLE chat_messages (
    id INTEGER PRIMARY KEY,
    username VARCHAR,
    message VARCHAR,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

## 📁 Project Structure

```
IITBBSR_TRABX/
│
├── main.py                 # FastAPI application & routes
├── models.py              # SQLAlchemy models
├── database.py            # Database configuration
├── requirements.txt       # Python dependencies
├── Dockerfile            # Docker configuration
├── README.md             # Project documentation
├── users.db              # SQLite database (auto-generated)
│
├── templates/            # HTML templates
│   ├── auth.html         # Authentication page
│   ├── dashboard.html    # Main dashboard
│   ├── alerts.html       # Alerts page
│   ├── chat.html         # Chat interface
│   ├── asteroids_by_date.html  # Search page
│   │
│   └── textures/         # 3D textures
│       └── planets/      # Planet texture files
│           ├── earth_daymap.jpg
│           ├── jupiter.jpg
│           ├── mars.jpg
│           ├── mercury.jpg
│           ├── moon.jpg
│           ├── neptune.jpg
│           ├── saturn.jpg
│           ├── saturn_ring.png
│           ├── sun.jpg
│           ├── uranus.jpg
│           └── venus.jpg
│
└── __pycache__/          # Python cache files
```

## 🖼 Screenshots

### Dashboard
The main dashboard features an interactive 3D solar system visualization powered by Three.js.

### Risk Alerts
Color-coded alerts system showing asteroids based on their calculated risk levels.

### Asteroid Search
Date-based search interface with detailed asteroid information and risk assessments.

### Community Chat
Real-time chat interface for users to discuss asteroid-related topics.

## 🐳 Docker Deployment

### Build Docker Image
```bash
docker build -t trabx-asteroid-tracker .
```

### Run Container
```bash
docker run -d -p 8000:8000 trabx-asteroid-tracker
```

## 🧪 Testing

### Manual Testing
1. Test user registration and login
2. Test asteroid search with various dates
3. Test risk calculation accuracy
4. Test WebSocket chat functionality
5. Test NASA API integration

### Example Test Cases
```python
# Test risk calculation
asteroid = {
    "diameter_km": 0.5,
    "velocity_km_s": 15.0,
    "miss_distance_km": 5000000,
    "hazardous": True
}
# Expected: MODERATE to HIGH risk
```

## 🔒 Security Considerations

### Current Implementation
- Basic password storage (plaintext)
- No session tokens
- No HTTPS enforcement

### Recommended Improvements
1. **Password Hashing**: Use bcrypt or Argon2
   ```python
   from passlib.context import CryptContext
   pwd_context = CryptContext(schemes=["bcrypt"])
   ```

2. **Session Management**: Implement JWT tokens
   ```python
   from fastapi_jwt_auth import AuthJWT
   ```

3. **HTTPS**: Deploy with SSL/TLS certificates
4. **Input Validation**: Add Pydantic models for request validation
5. **Rate Limiting**: Prevent API abuse
6. **CORS**: Configure proper CORS policies

## 🚧 Known Issues & Limitations

1. **Password Security**: Passwords are stored in plaintext
2. **Session Management**: No proper session handling
3. **Error Handling**: Limited error messages for users
4. **API Rate Limits**: No protection against NASA API rate limits
5. **Miss Distance**: Default value used in some calculations

## 🗺 Roadmap

### Phase 1 (Current)
- [x] Basic authentication
- [x] NASA API integration
- [x] Risk calculation system
- [x] 3D visualization
- [x] Real-time chat

### Phase 2 (Planned)
- [ ] Enhanced security (password hashing, JWT)
- [ ] Advanced filtering and sorting
- [ ] Export functionality (CSV, PDF)
- [ ] Email notifications for high-risk asteroids
- [ ] Mobile responsive design

### Phase 3 (Future)
- [ ] Machine learning risk prediction
- [ ] Historical trend analysis
- [ ] Multi-language support
- [ ] Mobile application
- [ ] Integration with additional space APIs

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Coding Standards
- Follow PEP 8 for Python code
- Add docstrings to functions
- Write meaningful commit messages
- Update documentation as needed

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **IIT Bhubaneswar Team** - Initial work - TRABX Project

## 🙏 Acknowledgments

- NASA for providing the NEO API
- FastAPI team for the excellent framework
- Three.js community for 3D visualization tools
- Planet texture sources for high-quality imagery

## 📞 Contact

For questions, suggestions, or issues:
- Create an issue in the GitHub repository
- Email: [your-email@example.com]
- Project Link: [https://github.com/yourusername/IITBBSR_TRABX](https://github.com/yourusername/IITBBSR_TRABX)

## 📚 Additional Resources

- [NASA NEO API Documentation](https://api.nasa.gov/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Three.js Documentation](https://threejs.org/docs/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)

---