# 🚀 Build & Deployment Guide

Complete guide for building and deploying the GovAI project.

## 📋 Prerequisites

- **Node.js 18+** and **pnpm** (or npm)
- **Python 3.10+**
- **Git**
- Environment variables configured (see SETUP.md)

---

## 🏗️ Building the Project

### Frontend (Next.js)

**Development Build:**
```bash
cd /Users/ap24/Hackwestern
pnpm install
pnpm dev
```

**Production Build:**
```bash
cd /Users/ap24/Hackwestern
pnpm install
pnpm build
pnpm start
```

The build creates an optimized production bundle in `.next/` directory.

### Backend (Python FastAPI)

**Development:**
```bash
cd /Users/ap24/Hackwestern
source venv/bin/activate  # or: python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
cd backend
python main.py
```

**Production:**
```bash
# Install dependencies
pip install -r requirements.txt

# Run with uvicorn (production server)
uvicorn backend.main:app --host 0.0.0.0 --port 8000
```

### Solana Program (Optional)

**Build Solana Program:**
```bash
cd govai_polls
anchor build
```

**Deploy to Devnet:**
```bash
anchor deploy --provider.cluster devnet
```

---

## 🌐 Deployment Options

### Option 1: Frontend on Vercel (Recommended)

**Step 1: Install Vercel CLI**
```bash
npm i -g vercel
```

**Step 2: Deploy**
```bash
cd /Users/ap24/Hackwestern
vercel
```

Or connect your GitHub repo to [Vercel Dashboard](https://vercel.com):
1. Go to vercel.com
2. Import your repository
3. Vercel auto-detects Next.js
4. Add environment variables in project settings

**Environment Variables for Vercel:**
```
NEXT_PUBLIC_BACKEND_URL=https://your-backend-url.com
NEXT_PUBLIC_SOLANA_RPC_URL=https://api.devnet.solana.com
NEXT_PUBLIC_SOLANA_NETWORK=devnet
```

**Build Command:** `pnpm build` (auto-detected)
**Output Directory:** `.next` (auto-detected)

---

### Option 2: Backend on Render

**Using render.yaml (Already configured):**

1. **Push to GitHub**
2. **Connect to Render:**
   - Go to [render.com](https://render.com)
   - New → Blueprint
   - Connect your GitHub repo
   - Render will detect `render.yaml`

3. **Set Environment Variables in Render Dashboard:**
   ```
   SUPABASE_URL=your_supabase_url
   SUPABASE_KEY=your_supabase_key
   GEMINI_API_KEY=your_gemini_api_key
   PORT=8000
   ```

**Manual Render Setup:**
- Service Type: Web Service
- Environment: Python 3
- Build Command: `pip install -r requirements.txt`
- Start Command: `cd backend && python main.py`

---

### Option 3: Backend on Railway

**Step 1: Create Procfile**
```bash
echo "web: uvicorn backend.main:app --host 0.0.0.0 --port \$PORT" > Procfile
```

**Step 2: Deploy**
1. Go to [railway.app](https://railway.app)
2. New Project → Deploy from GitHub
3. Add environment variables
4. Railway auto-detects Python and runs the Procfile

---

### Option 4: Docker Deployment

**Create Dockerfile for Backend:**
```dockerfile
FROM python:3.10-slim

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application
COPY . .

# Expose port
EXPOSE 8000

# Run application
CMD ["uvicorn", "backend.main:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Build and Run:**
```bash
docker build -t govai-backend .
docker run -p 8000:8000 --env-file .env govai-backend
```

**Create docker-compose.yml (Full Stack):**
```yaml
version: '3.8'

services:
  backend:
    build: .
    ports:
      - "8000:8000"
    env_file:
      - .env
    environment:
      - PORT=8000

  frontend:
    build:
      context: .
      dockerfile: Dockerfile.frontend
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_BACKEND_URL=http://backend:8000
```

---

## 🔧 Environment Variables Setup

### Frontend (.env.local)
```bash
NEXT_PUBLIC_BACKEND_URL=https://your-backend-url.com
NEXT_PUBLIC_SOLANA_RPC_URL=https://api.devnet.solana.com
NEXT_PUBLIC_SOLANA_NETWORK=devnet
```

### Backend (.env)
```bash
SUPABASE_URL=https://xxx.supabase.co
SUPABASE_KEY=your_anon_key
GEMINI_API_KEY=your_gemini_api_key
FRONTEND_URL=https://your-frontend-url.com
PORT=8000
```

---

## ✅ Pre-Deployment Checklist

- [ ] All environment variables are set
- [ ] Database tables are created in Supabase
- [ ] Frontend builds successfully (`pnpm build`)
- [ ] Backend runs locally (`python backend/main.py`)
- [ ] CORS is configured for production URLs
- [ ] Solana program is deployed (if using on-chain features)
- [ ] API keys are valid and have proper quotas

---

## 🧪 Testing Production Build Locally

**Test Frontend:**
```bash
pnpm build
pnpm start
# Visit http://localhost:3000
```

**Test Backend:**
```bash
uvicorn backend.main:app --host 0.0.0.0 --port 8000
# Test: curl http://localhost:8000/health
```

---

## 📊 Current Deployment Status

According to README.md:
- **Frontend:** Deployed at [govai-plum.vercel.app](https://govai-plum.vercel.app)
- **Backend:** Configured for Render (see `render.yaml`)

---

## 🔗 Quick Deploy Commands

**One-Command Local Build:**
```bash
# Frontend
cd /Users/ap24/Hackwestern && pnpm install && pnpm build

# Backend
cd /Users/ap24/Hackwestern && pip install -r requirements.txt
```

**Deploy to Vercel:**
```bash
vercel --prod
```

**Deploy to Render:**
```bash
# Just push to GitHub, Render auto-deploys from render.yaml
git push origin main
```

---

## 🆘 Troubleshooting

**Build Fails:**
- Check Node.js version: `node --version` (need 18+)
- Clear cache: `rm -rf .next node_modules && pnpm install`
- Check TypeScript errors: `pnpm lint`

**Backend Won't Start:**
- Verify environment variables are set
- Check Python version: `python --version` (need 3.10+)
- Test database connection: `python test_connection.py`

**CORS Errors:**
- Update `FRONTEND_URL` in backend `.env`
- Add frontend URL to CORS allowed origins in `backend/main.py`

---

## 📚 Additional Resources

- [Next.js Deployment](https://nextjs.org/docs/deployment)
- [Vercel Documentation](https://vercel.com/docs)
- [Render Documentation](https://render.com/docs)
- [FastAPI Deployment](https://fastapi.tiangolo.com/deployment/)

