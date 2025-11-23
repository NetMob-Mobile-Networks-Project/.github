# Polaris - Mobile Network Quality of Experience (QoE) Monitoring System

<div align="center">

![Polaris](https://img.shields.io/badge/Polaris-Network%20Monitoring-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Version](https://img.shields.io/badge/version-1.0-orange)

**A comprehensive end-to-end solution for monitoring and analyzing mobile network performance from the user's perspective**

Named after the North Star (Polaris), this system serves as a guiding tool for measuring and analyzing network Quality of Experience (QoE) metrics.

</div>

---

## 📋 Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Quick Start with Docker](#quick-start-with-docker)
  - [Manual Installation](#manual-installation)
- [Component Details](#component-details)
  - [Polaris Client (Android)](#polaris-client-android)
  - [Polaris Server (Go Backend)](#polaris-server-go-backend)
  - [Polaris Web (Next.js Dashboard)](#polaris-web-nextjs-dashboard)
- [API Documentation](#api-documentation)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## 🎯 Overview

Polaris is a complete mobile network monitoring and analysis platform designed to measure Quality of Experience (QoE) from end-user devices. The system consists of three main components working together to collect, store, analyze, and visualize network performance data.

### Key Capabilities

- **Real-time Network Monitoring**: Continuous collection of network parameters including signal strength, cell information, and location data
- **Automated Performance Testing**: Comprehensive test suite for HTTP, Ping, DNS, Web, and SMS performance
- **Data Visualization**: Interactive web dashboard with maps, charts, and analytics
- **Scalable Architecture**: Clean architecture design supporting multiple concurrent devices
- **Background Operation**: Android client operates efficiently in the background with minimal battery impact

---

## 🏗️ System Architecture

```
┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐
│                 │         │                 │         │                 │
│  Polaris Client │────────▶│  Polaris Server │◀────────│  Polaris Web    │
│   (Android)     │  HTTP   │   (Go/MySQL)    │  REST   │   (Next.js)     │
│                 │         │                 │         │                 │
└─────────────────┘         └─────────────────┘         └─────────────────┘
      │                              │                            │
      │                              │                            │
      │ Collects Network Data        │ Stores & Processes         │ Visualizes & Manages
      │ Runs Performance Tests       │ Provides API               │ User Interface
      │ Uploads to Server            │ Authentication             │ Analytics Dashboard
```

### Data Flow

1. **Collection**: Android client collects network measurements and runs performance tests
2. **Storage**: Data is stored locally on the device and periodically uploaded to the server
3. **Processing**: Server stores data in MySQL database and provides RESTful API
4. **Visualization**: Web dashboard fetches data and presents interactive visualizations

---

## ✨ Features

### 📱 Mobile Client Features

- **Network Parameter Monitoring**
  - Real-time location tracking (GPS coordinates)
  - Cellular technology detection (2G/3G/4G/5G)
  - Cell identifiers (PLMN-Id, LAC, RAC, TAC, Cell ID)
  - Frequency band monitoring (ARFCN)
  - Signal quality metrics (RSRP, RSRQ, RSCP, RxLev)

- **Automated Testing Suite**
  - HTTP Download/Upload throughput tests
  - Ping latency measurements
  - DNS resolution time tests
  - Web page loading time tests
  - SMS delivery time tests

- **Background Operation**
  - Periodic data collection (configurable intervals)
  - Automatic data synchronization
  - Local database caching
  - WorkManager-based background tasks

### 🖥️ Server Features

- **RESTful API**
  - JWT-based authentication
  - Role-based access control (Admin/User)
  - Comprehensive metrics endpoints
  - Data export capabilities (CSV, KML)

- **Database Management**
  - MySQL database with optimized schema
  - Type-safe queries using sqlc
  - Efficient indexing for time-series data
  - Support for JSON fields for flexible data storage

- **Configuration Management**
  - Remote configuration for mobile clients
  - Configurable sampling intervals
  - Test type selection

### 🌐 Web Dashboard Features

- **Real-time Analytics**
  - Dynamic metrics tables with pagination
  - Time-based filtering (Last Hour, 24 Hours, 7 Days, 30 Days)
  - Multiple metric types visualization
  - CSV export functionality

- **Interactive Network Map**
  - Real-time coverage visualization using Leaflet
  - Color-coded signal strength indicators
  - Customizable performance thresholds
  - KML export for external mapping tools

- **Administrative Tools**
  - User management (Admin only)
  - System configuration management
  - Data collection settings
  - Role-based access control

---

## 🛠️ Technology Stack

### Polaris Client
- **Language**: Kotlin
- **Framework**: Android SDK
- **Architecture**: Clean Architecture (MVVM)
- **Database**: Room (SQLite)
- **Networking**: Retrofit, OkHttp
- **Background Tasks**: WorkManager
- **UI**: Jetpack Compose, Material Design 3
- **Minimum SDK**: API 28 (Android 9.0)
- **Target SDK**: API 34 (Android 14)

### Polaris Server
- **Language**: Go 1.23+
- **Framework**: Gorilla Mux
- **Database**: MySQL 5.7+
- **Query Builder**: sqlc (type-safe SQL)
- **Authentication**: JWT (golang-jwt/jwt)
- **Password Hashing**: bcrypt (golang.org/x/crypto)

### Polaris Web
- **Framework**: Next.js 15.2.3
- **Language**: TypeScript
- **UI Library**: React 19
- **Styling**: Tailwind CSS 4
- **Maps**: Leaflet, React-Leaflet
- **Charts**: Chart.js
- **HTTP Client**: Axios
- **Forms**: React Hook Form, Zod

---

## 📁 Project Structure

```
Mobile/
├── polaris-client-main/          # Android mobile application
│   ├── app/                      # Main application module
│   ├── data/                     # Data layer module
│   ├── domain/                   # Domain layer module
│   └── readme.md                 # Client-specific documentation
│
├── polaris-server-main/          # Go backend server
│   ├── cmd/polaris-server/       # Application entry point
│   ├── internal/
│   │   ├── api/                  # HTTP handlers and routes
│   │   └── storage/              # Database layer
│   │       ├── db/               # Generated sqlc code
│   │       ├── query/            # SQL queries
│   │       └── schema/           # Database schema
│   ├── compose.yaml              # Docker Compose configuration
│   └── README.md                 # Server-specific documentation
│
├── polaris-web-main/             # Next.js web dashboard
│   ├── src/
│   │   ├── app/                  # Next.js App Router pages
│   │   ├── components/           # React components
│   │   └── lib/                  # Utilities and services
│   ├── docker-compose.yml        # Docker Compose configuration
│   └── README.md                 # Web-specific documentation
│
├── Final Report.pdf              # Project documentation
├── Final Manual.pdf              # User manual
└── README.md                     # This file
```

---

## 🚀 Getting Started

### Prerequisites

Before you begin, ensure you have the following installed:

- **For Client Development**:
  - Android Studio (latest version)
  - JDK 8 or higher
  - Android SDK (API 28+)

- **For Server Development**:
  - Go 1.23 or later
  - MySQL 5.7 or later
  - sqlc CLI tool

- **For Web Development**:
  - Node.js 18 or later
  - npm, yarn, pnpm, or bun

- **For Docker Deployment**:
  - Docker Engine 20.10+
  - Docker Compose 2.0+

### Quick Start with Docker

The easiest way to get started is using Docker Compose:

#### 1. Start the Server and Database

```bash
cd polaris-server-main
docker-compose up -d
```

This will start:
- MySQL database on port 3306
- Polaris Server API on port 8080

#### 2. Start the Web Dashboard

```bash
cd polaris-web-main
docker-compose up -d
```

The web dashboard will be available at `http://localhost:80`

#### 3. Build and Install Android Client

```bash
cd polaris-client-main
# Open in Android Studio and build
# Or use Gradle:
./gradlew assembleRelease
```

The APK will be generated in `app/release/app-release.apk`

### Manual Installation

#### Server Setup

1. **Clone and navigate to server directory**:
```bash
cd polaris-server-main
```

2. **Set up environment variables**:
```bash
export DB_USER=root
export DB_PASS=your_password
export DB_HOST=localhost
export DB_PORT=3306
export DB_NAME=polaris
export JWT_SECRET=your-secret-key-here
export SERVER_PORT=8080
```

3. **Initialize database**:
```bash
mysql -u root -p < internal/storage/schema/schema.sql
```

4. **Generate sqlc code** (if needed):
```bash
cd internal/storage
sqlc generate
```

5. **Run the server**:
```bash
go run cmd/polaris-server/main.go
```

#### Web Dashboard Setup

1. **Navigate to web directory**:
```bash
cd polaris-web-main
```

2. **Install dependencies**:
```bash
npm install
```

3. **Configure environment**:
Create `.env.local`:
```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:8080/api/v1
```

4. **Run development server**:
```bash
npm run dev
```

Access the dashboard at `http://localhost:3000`

#### Android Client Setup

1. **Open in Android Studio**:
   - Open `polaris-client-main` directory
   - Sync Gradle files
   - Wait for dependencies to download

2. **Configure API endpoint**:
   Edit `app/src/main/java/com/yourdomain/polarsclient/Polaris.kt`:
   ```kotlin
   private val BASE_URL = "http://your-server-ip:8080/"
   ```

3. **Build and run**:
   - Connect an Android device or start an emulator
   - Click "Run" in Android Studio

---

## 📦 Component Details

### Polaris Client (Android)

The Android client is built using Clean Architecture principles with three main layers:

- **Presentation Layer**: UI components using Jetpack Compose and MVVM pattern
- **Domain Layer**: Business logic and use cases (framework-independent)
- **Data Layer**: Repository implementations, local database (Room), and remote API (Retrofit)

**Key Features**:
- Automatic background data collection every 15 minutes (configurable)
- Local caching with Room database
- Periodic upload to server using WorkManager
- Support for all major cellular technologies (2G/3G/4G/5G)

**Permissions Required**:
- `ACCESS_FINE_LOCATION` - For GPS coordinates
- `INTERNET` - For network tests and data upload
- `SEND_SMS` - For SMS test functionality
- `ACCESS_NETWORK_STATE` - For network information

For detailed client documentation, see [polaris-client-main/readme.md](polaris-client-main/readme.md)

### Polaris Server (Go Backend)

The server provides a RESTful API built with Go and MySQL. It uses sqlc for type-safe database operations.

**API Endpoints**:

**Public Endpoints**:
- `POST /api/v1/auth/login` - User authentication
- `POST /api/v1/measurements/upload` - Upload network measurements
- `POST /api/v1/tests/*/upload` - Upload test results
- `GET /api/v1/config` - Get client configuration

**Protected Endpoints** (require JWT):
- `GET /api/v1/auth/me` - Get user profile
- `GET /api/v1/metrics/*` - Various metrics endpoints
- `GET /api/v1/export/csv` - Export data as CSV
- `GET /api/v1/export/kml` - Export map data as KML

**Admin Endpoints** (require admin role):
- `GET /api/v1/admin/users` - List users
- `POST /api/v1/admin/users` - Create user
- `DELETE /api/v1/admin/users/{id}` - Delete user
- `PUT /api/v1/admin/config` - Update system configuration

**Database Schema**:
- `users` - User accounts and authentication
- `client_config` - Remote configuration for clients
- `network_measurements` - Network parameter data
- `http_test_results` - HTTP download/upload test results
- `ping_test_results` - Ping test results
- `dns_test_results` - DNS resolution test results
- `web_test_results` - Web page loading test results
- `sms_test_results` - SMS delivery test results

For detailed server documentation, see [polaris-server-main/README.md](polaris-server-main/README.md)

### Polaris Web (Next.js Dashboard)

The web dashboard is a modern Next.js application providing real-time visualization and management capabilities.

**Main Pages**:
- `/auth/login` - User authentication
- `/dashboard` - Overview dashboard with KPIs
- `/dashboard/analytics` - Detailed analytics and metrics tables
- `/dashboard/map` - Interactive network coverage map
- `/dashboard/settings` - Administrative settings (Admin only)

**Key Components**:
- **ProtectedRoute**: Route protection with authentication
- **NetworkMap**: Interactive Leaflet-based map visualization
- **MetricsTable**: Dynamic, paginated metrics display
- **Charts**: Network distribution and performance charts

For detailed web documentation, see [polaris-web-main/README.md](polaris-web-main/README.md)

---

## 🔧 Configuration

### Server Configuration

Environment variables for the server:

```bash
# Database
DB_USER=root
DB_PASS=your_password
DB_HOST=localhost
DB_PORT=3306
DB_NAME=polaris

# Server
SERVER_PORT=8080

# Security
JWT_SECRET=your-secret-key-here-change-in-production

# API
API_VERSION=v1
```

### Client Configuration

The client configuration is managed remotely through the server. Admins can configure:

- **Sampling Interval**: How often to collect network measurements (in seconds)
- **Test Types**: Which tests to run (HTTP Download, HTTP Upload, Ping, DNS, Web, SMS)

Configuration is fetched automatically by the client on startup and periodically.

### Web Dashboard Configuration

Environment variables:

```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:8080/api/v1
NODE_ENV=development
```

---

## 🚢 Deployment

### Production Deployment

#### Server Deployment

1. **Build Docker image**:
```bash
cd polaris-server-main
docker build -t polaris-server:latest .
```

2. **Deploy with Docker Compose**:
```bash
docker-compose up -d
```

3. **Or deploy manually**:
```bash
go build -o polaris-server cmd/polaris-server/main.go
./polaris-server
```

#### Web Dashboard Deployment

1. **Build production bundle**:
```bash
cd polaris-web-main
npm run build
```

2. **Deploy with Docker**:
```bash
docker-compose up -d
```

3. **Or deploy to Vercel/Netlify**:
```bash
# Configure environment variables in your hosting platform
# Deploy using their CLI or web interface
```

#### Android Client Deployment

1. **Generate signed APK**:
   - In Android Studio: Build → Generate Signed Bundle / APK
   - Follow the signing wizard
   - Distribute the APK to users

2. **Or publish to Google Play Store**:
   - Create a release build
   - Upload to Play Console
   - Follow Play Store publishing guidelines

### Security Considerations

- Change default JWT secret in production
- Use HTTPS for all API communications
- Implement proper CORS policies
- Use strong database passwords
- Enable database encryption at rest
- Implement rate limiting on API endpoints
- Regular security updates for dependencies

---

## 📊 API Documentation

### Authentication

All protected endpoints require a JWT token in the Authorization header:

```
Authorization: Bearer <token>
```

### Example API Calls

**Login**:
```bash
curl -X POST http://localhost:8080/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password"}'
```

**Get Metrics**:
```bash
curl -X GET http://localhost:8080/api/v1/metrics/detailed-list \
  -H "Authorization: Bearer <token>"
```

**Upload Measurements**:
```bash
curl -X POST http://localhost:8080/api/v1/measurements/upload \
  -H "Content-Type: application/json" \
  -d '{"device_id":"device-123","measurements":[...]}'
```

For complete API documentation, refer to the server code in `polaris-server-main/internal/api/`.

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow the existing code style and architecture patterns
- Write tests for new features
- Update documentation as needed
- Ensure all components work together
- Test on multiple Android versions (if modifying client)

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file in `polaris-web-main` for details.

---

## 📞 Contact

For questions, issues, or contributions:

- **Project Repository**: [GitHub Repository URL]
- **Issues**: [GitHub Issues URL]
- **Documentation**: See `Final Report.pdf` and `Final Manual.pdf` for detailed documentation

---

## 🙏 Acknowledgments

- Developed as part of the NetMob Mobile Networks Project
- Special thanks to all contributors and maintainers
- Built with modern best practices and clean architecture principles

---

<div align="center">

**Version 1.0** - Bahman 1403 (February 2025)

Made with ❤️ for mobile network monitoring

</div>

