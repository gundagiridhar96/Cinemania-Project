# 🎬 CINEMANIA — OTT Platform

A full-stack Netflix/Amazon Prime-style OTT platform with tiered subscription logic.

---

## 🛠 TECH STACK

| Layer    | Technology                        |
|----------|-----------------------------------|
| Backend  | Node.js, Express.js               |
| Database | MySQL                             |
| Auth     | JWT (JSON Web Tokens) + bcrypt    |
| Frontend | Vanilla HTML/CSS/JS               |
| Payments | Stripe-ready (mock in dev)        |

---

## 📁 PROJECT STRUCTURE

```
cinemania/
├── backend/
│   ├── config/
│   │   ├── db.js              # MySQL connection pool
│   │   └── schema.sql         # Database schema + seed data
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── contentController.js
│   │   ├── subscriptionController.js
│   │   └── userController.js
│   ├── middleware/
│   │   └── auth.js            # JWT protect + adminOnly
│   ├── routes/
│   │   ├── auth.js
│   │   ├── content.js
│   │   ├── subscriptions.js
│   │   └── users.js
│   ├── .env                   # Environment variables ← EDIT THIS
│   ├── package.json
│   └── server.js
│
└── frontend/
    ├── css/
    │   └── style.css
    ├── js/
    │   ├── api.js             # API helper
    │   └── app.js             # Main app logic
    ├── pages/
    │   ├── movies.html
    │   ├── series.html
    │   ├── categories.html
    │   ├── watchlist.html
    │   ├── subscription.html
    │   ├── profile.html
    │   └── admin.html
    └── index.html
```

---

## ⚡ STEP-BY-STEP SETUP

### STEP 1 — Install Required Software

Make sure these are installed:
- ✅ Node.js (v18+) — https://nodejs.org
- ✅ MySQL (v8+) — https://dev.mysql.com/downloads/
- ✅ VS Code — https://code.visualstudio.com

### STEP 2 — Install Node Packages

Open terminal inside `backend/` folder:

```bash
cd cinemania/backend
npm install
```

This installs: express, mysql2, bcryptjs, jsonwebtoken, cors, dotenv, nodemon

### STEP 3 — Setup MySQL Database

**Option A: MySQL Workbench**
1. Open MySQL Workbench
2. Connect to your server
3. File → Open SQL Script → select `backend/config/schema.sql`
4. Click ⚡ (Execute All)

**Option B: Command Line**
```bash
mysql -u root -p < backend/config/schema.sql
```

### STEP 4 — Configure Environment

Edit `backend/.env`:

```env
PORT=5000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=YOUR_MYSQL_PASSWORD_HERE   ← change this
DB_NAME=cinemania_db
JWT_SECRET=cinemania_super_secret_jwt_key_2024
JWT_EXPIRES_IN=7d
```

### STEP 5 — Start the Server

```bash
cd backend
npm run dev
```

You should see:
```
🎬 CINEMANIA SERVER RUNNING
📡 API: http://localhost:5000/api
🌐 App: http://localhost:5000
```

### STEP 6 — Open the App

Open your browser and go to: **http://localhost:5000**

---

## 🔑 DEFAULT ADMIN CREDENTIALS

| Field    | Value               |
|----------|---------------------|
| Email    | admin@cinemania.com |
| Password | password            |

> ⚠️ Change this password after first login!

**To access admin panel:** Login → click avatar → "Admin Panel"

---

## 🌟 FEATURES

### 🎬 User Features
- ✅ Register / Login with JWT auth
- ✅ Browse movies, series, documentaries
- ✅ Search content
- ✅ Filter by genre, language, type
- ✅ Watchlist (add/remove)
- ✅ Watch history
- ✅ Content detail modal with metadata

### 👑 Subscription Tiers

| Plan     | Price | Quality | Screens | Downloads |
|----------|-------|---------|---------|-----------|
| Free     | ₹0    | SD      | 1       | ✗         |
| Basic    | ₹99   | HD      | 1       | ✗         |
| Standard | ₹199  | Full HD | 2       | ✓         |
| Premium  | ₹499  | 4K      | 4       | ✓         |

### ⚙️ Admin Features
- ✅ Dashboard with live stats (users, subs, revenue, content)
- ✅ Add / Delete content
- ✅ View all users + their plan status
- ✅ View all subscription transactions

---

## 📡 API ENDPOINTS

### Auth
| Method | Endpoint            | Description        |
|--------|---------------------|--------------------|
| POST   | /api/auth/register  | Create account     |
| POST   | /api/auth/login     | Login              |
| GET    | /api/auth/me        | Get current user   |

### Content
| Method | Endpoint           | Description            |
|--------|--------------------|------------------------|
| GET    | /api/content       | List (filterable)      |
| GET    | /api/content/:id   | Single content         |
| POST   | /api/content       | Create (admin)         |
| PUT    | /api/content/:id   | Update (admin)         |
| DELETE | /api/content/:id   | Delete (admin)         |

### Subscriptions
| Method | Endpoint                    | Description          |
|--------|-----------------------------|----------------------|
| GET    | /api/subscriptions/plans    | All plans            |
| POST   | /api/subscriptions/subscribe| Subscribe to plan    |
| GET    | /api/subscriptions/my       | User's subscriptions |
| POST   | /api/subscriptions/cancel   | Cancel subscription  |

### Users
| Method | Endpoint                    | Description        |
|--------|-----------------------------|--------------------|
| GET    | /api/users/watchlist        | Get watchlist      |
| POST   | /api/users/watchlist/:id    | Add to watchlist   |
| DELETE | /api/users/watchlist/:id    | Remove from list   |
| GET    | /api/users/history          | Watch history      |
| PUT    | /api/users/profile          | Update profile     |

---

## 🔧 COMMON ISSUES & FIXES

**"ER_NOT_SUPPORTED_AUTH_MODE" MySQL error:**
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
FLUSH PRIVILEGES;
```

**Port 5000 already in use:**
Change `PORT=5001` in `.env`

**Cannot find module 'express':**
```bash
cd backend && npm install
```

**Frontend shows blank / API errors:**
- Make sure backend is running on port 5000
- Check browser console for errors
- Verify MySQL is running

---

## 🚀 PRODUCTION DEPLOYMENT (Optional)

For hosting on a server:
1. Set `NODE_ENV=production` in `.env`
2. Use PM2: `npm install -g pm2 && pm2 start server.js`
3. Use Nginx as reverse proxy
4. Use environment variables for secrets

---

Built with ❤️ as a Subscription-Based Membership Engine project.
