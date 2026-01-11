# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) and other AI models when working with code in this repository.

---

## Project Overview
**AgroPrice Insight** — Sistem za automatsko preuzimanje, skladištenje i vizuelizaciju mesečnih indeksa cena proizvođača poljoprivrednih proizvoda sa zvaničnog Open Data API-ja Srbije.

Projekat omogućava:
- Automatski import podataka sa Open Data API
- Dashboard vizuelizacije trendova
- Filtriranje po periodima i grupama proizvoda
- REST API za integracije
- Administratorski panel

---

## Technology Stack
- **Frontend:** React + TypeScript
  - Styling: (To be determined - CSS framework)
  - State Management: (To be determined)

- **Backend:** Node.js / Express
  - API layer
  - ETL process for data synchronization

- **Database:** PostgreSQL
  - ORM: (To be determined - Prisma/Sequelize/TypeORM)

- **Testing:** (To be determined)
  - Unit testing tool
  - E2E testing tool

- **Build/Deploy:** Docker
  - CI/CD: (To be determined)
  - Hosting: (To be determined)

**Data Source:** 
- Open Data API Srbije: https://opendata.stat.gov.rs/data/WcfJsonRestService.Service1.svc/dataset/03020203IND01/1/json

---

## Architecture

### System Overview
```
┌─────────────────┐
│   Open Data     │
│   API Serbia    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐      ┌─────────────────┐
│   ETL Process   │─────▶│   PostgreSQL    │
└─────────────────┘      └────────┬────────┘
                                  │
                         ┌────────┴────────┐
                         ▼                 ▼
                  ┌──────────┐      ┌──────────┐
                  │   API    │      │  Admin   │
                  │  Layer   │      │  Panel   │
                  └─────┬────┘      └──────────┘
                        │
                        ▼
                  ┌──────────┐
                  │Dashboard │
                  │  React   │
                  └──────────┘
```

### Key Directories
```
/ilija
├── /backend          # API i ETL logika
│   ├── /src
│   ├── /routes       # API endpoints
│   ├── /services     # Business logic
│   └── /models       # Database models
├── /frontend         # Dashboard aplikacija
│   ├── /src
│   ├── /components   # React komponente
│   └── /pages        # Stranice aplikacije
├── /docs             # AI_TEMPLATE dokumentacija
└── /docker           # Docker konfiguracija
```

---

## Project Roles & Organization

This project uses a multi-role AI collaboration framework with the following roles:

### Role Files
1. **PROJECT_DIRECTOR.md** - Strategic oversight, priorities, stakeholder communication
2. **DIRECTOR_OF_DEVELOPMENT.md** - Technical architecture, code quality, task planning
3. **DEVELOPMENT_TEAM.md** - Implementation, coding, testing, daily progress

### 🤖 AI Model Role Instructions

**IMPORTANT:** When working on this project, YOU as an AI model should:

1. **Check PROJECT_STATUS.md FIRST** to understand current project state
2. **Identify your role based on the task:**
   - Strategic/planning questions → Read PROJECT_DIRECTOR.md
   - Technical architecture → Read DIRECTOR_OF_DEVELOPMENT.md
   - Implementation/coding → Read and UPDATE DEVELOPMENT_TEAM.md

3. **Always update the relevant role file** after completing work
4. **Add an entry to PROJECT_STATUS.md** for significant changes

**Default workflow:**
```
1. Read PROJECT_STATUS.md → Understand where we are
2. Read DIRECTOR_OF_DEVELOPMENT.md → Know current technical priorities
3. Read DEVELOPMENT_TEAM.md → Check task board and current sprint
4. Do the work
5. Update DEVELOPMENT_TEAM.md → Log what you did
6. Update PROJECT_STATUS.md → Record the change
```

---

## Project Status Tracking

### Master Status Log
**File:** `PROJECT_STATUS.md`

This is the **single source of truth** for project progress. All roles update this file chronologically.

Format:
```
[YYYY-MM-DD HH:MM] - [Brief description]
Status: ✅ Done / 🔄 In Progress / ⏳ Planned / ❌ Blocked
Role: [Director/Development/Team]
Details: [What was done, decisions made, etc.]
```

---

## Common Development Commands

### Setup
```bash
# Backend setup
cd backend
npm install
cp .env.example .env  # Configure environment variables
npm run migrate       # Run database migrations

# Frontend setup
cd frontend
npm install
```

### Running Locally
```bash
# Start backend (API + ETL)
cd backend
npm run dev           # Development mode with hot reload
# Usually runs on: http://localhost:3000

# Start frontend (Dashboard)
cd frontend
npm run dev
# Usually runs on: http://localhost:5173 (Vite default)
```

### Testing
```bash
# Backend tests
cd backend
npm test              # Run all tests
npm run test:watch    # Watch mode

# Frontend tests
cd frontend
npm test
```

### Building
```bash
# Build for production
docker-compose build
docker-compose up -d

# Or separately:
cd backend && npm run build
cd frontend && npm run build
```

---

## Environment Variables

**Backend (.env):**
```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/agroprice
DB_HOST=localhost
DB_PORT=5432
DB_NAME=agroprice
DB_USER=postgres
DB_PASSWORD=your_password

# API Configuration
PORT=3000
NODE_ENV=development

# Open Data API
OPENDATA_API_URL=https://opendata.stat.gov.rs/data/WcfJsonRestService.Service1.svc/dataset/03020203IND01/1/json
SYNC_INTERVAL=daily  # How often to sync data

# Authentication (if needed)
JWT_SECRET=your_jwt_secret
```

**Frontend (.env):**
```env
VITE_API_URL=http://localhost:3000/api
```

---

## Code Architecture Patterns

### ETL Process Pattern
The backend uses an ETL (Extract, Transform, Load) pattern for data synchronization:

1. **Extract:** Fetch data from Open Data API
2. **Transform:** Parse JSON, validate, normalize data structure
3. **Load:** Insert/Update PostgreSQL database

**Implementation location:** `/backend/src/services/etl/`

### API Layer Pattern
REST API follows standard CRUD operations:
- `GET /api/prices` - List all price indices
- `GET /api/prices/:id` - Get specific price index
- `GET /api/prices/filter` - Filter by date range, product category
- `POST /api/sync` - Trigger manual data synchronization (admin only)

**Implementation location:** `/backend/src/routes/`

---

## Important Implementation Notes

### Data Synchronization Strategy
- **Automatic sync:** Runs daily via cron job
- **Manual sync:** Available through admin panel
- **Conflict resolution:** Latest API data always overwrites local data
- **History preservation:** Old data is archived, not deleted

### Performance Considerations
- Database indices on date and product category fields
- Caching layer for frequently accessed data (Redis - planned)
- Pagination for large data sets (100 items per page)

---

## Key Files to Understand

### Project Documentation (Root)
- `README.md` - Quick start guide
- `CLAUDE.md` - THIS FILE - AI guidance
- `PROJECT_STATUS.md` - Master status log
- `PROJECT_DIRECTOR.md` - Strategic direction
- `DIRECTOR_OF_DEVELOPMENT.md` - Technical leadership
- `DEVELOPMENT_TEAM.md` - Implementation workspace

### Main Source Files
**Backend:**
- `/backend/src/server.js` - Main entry point
- `/backend/src/routes/prices.js` - Price API routes
- `/backend/src/services/etl/opendata-sync.js` - ETL logic
- `/backend/src/models/PriceIndex.js` - Database model

**Frontend:**
- `/frontend/src/App.tsx` - Main React app
- `/frontend/src/pages/Dashboard.tsx` - Main dashboard
- `/frontend/src/components/PriceChart.tsx` - Visualization component

---

## Common Pitfalls

1. **API Rate Limiting:** Open Data API may have rate limits. Implement retry logic with exponential backoff.

2. **Date Format Consistency:** Ensure dates are stored in UTC in database, converted to local timezone for display.

3. **Data Validation:** Always validate data from external API before inserting into database.

4. **Environment Variables:** Never commit `.env` files. Use `.env.example` as template.

---

## Development Workflow Notes

### Code Style
- **JavaScript/TypeScript:** ESLint + Prettier
- **Naming:** camelCase for variables/functions, PascalCase for components/classes
- **Commits:** Conventional commits format (`feat:`, `fix:`, `docs:`, etc.)

### Git Workflow
```bash
# Feature development
git checkout -b feature/description
# ... make changes ...
git add .
git commit -m "feat: description"
git push origin feature/description
# ... create pull request ...
```

---

## Future Enhancements (Backlog)

- [ ] PDF/Excel export functionality for reports
- [ ] Email notifications for significant price changes
- [ ] Multi-language support (English, Serbian)
- [ ] Mobile app (React Native)
- [ ] Advanced analytics (ML predictions)
- [ ] Public API with authentication

---

## Instructions for Customizing This Template

This template has been customized for the AgroPrice Insight project. The following placeholders have been replaced:

✅ **Completed Customizations:**
- Project name: AgroPrice Insight
- Technology stack: Node.js, React, PostgreSQL, Docker
- Key directories defined
- Development commands outlined
- Data source identified

⏳ **To Be Determined:**
- Specific CSS framework for frontend
- State management solution
- ORM choice
- Testing frameworks
- CI/CD platform
- Hosting provider

**Next Steps:**
1. Review and approve this documentation structure
2. Create directory structure (`/backend`, `/frontend`, `/docs`)
3. Initialize PROJECT_DIRECTOR.md with initial vision
4. Initialize DIRECTOR_OF_DEVELOPMENT.md with technical priorities
5. Initialize DEVELOPMENT_TEAM.md with first sprint tasks
