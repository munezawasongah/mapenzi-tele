# mapenziTELE 🔥

> Free casual dating platform — Node.js + PostgreSQL + Socket.IO

---

## 🚀 Deploy to Railway in 5 Steps

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/mapenzitele.git
git push -u origin main
```

### 2. Create Railway Project
1. Go to [railway.app](https://railway.app) → **New Project**
2. Choose **Deploy from GitHub repo** → select `mapenzitele`
3. Click **Add Service** → **Database** → **PostgreSQL**
4. Railway auto-sets `DATABASE_URL` in your environment

### 3. Set Environment Variables
In Railway dashboard → your service → **Variables**, add:
```
JWT_SECRET=<generate with: node -e "console.log(require('crypto').randomBytes(48).toString('hex'))">
APP_URL=https://YOUR-APP.up.railway.app
CLIENT_URL=https://YOUR-APP.up.railway.app
NODE_ENV=production
UPLOAD_DIR=/data/uploads   # attach a Railway Volume at /data to keep photos
```

### 4. Run Database Migration
In Railway → your service → **Shell**:
```bash
npm run migrate
```

### 5. Go Live ✅
Railway auto-deploys on every push to `main`.

---

## 🛠 Local Development

```bash
npm install
cp .env.example .env
# Fill in .env values
npm run migrate
npm run dev
```
Open http://localhost:3000

---

## 📁 Project Structure
```
mapenzitele/
├── server.js           # Express + Socket.IO entry point
├── routes/
│   ├── auth.js         # Register, login, /me
│   ├── users.js        # Discover, profile update, location
│   ├── matches.js      # Sparks, matches, who-liked-me
│   ├── messages.js     # Chat inbox + send
│   ├── photos.js       # Upload, delete, set primary
│   └── push.js         # Push notification token registration
├── middleware/
│   └── auth.js         # JWT verify
├── db/
│   ├── index.js        # PostgreSQL pool
│   └── migrate.js      # Schema migration
├── public/
│   ├── index.html      # Full SPA frontend
│   └── uploads/        # User photo files (auto-created)
├── .env.example
├── railway.json
└── package.json
```

## 🔒 Security Features
- Passwords hashed with bcrypt (12 rounds)
- JWT tokens (30-day expiry)
- Rate limiting on all endpoints
- Helmet.js HTTP headers
- Input validation on all routes
