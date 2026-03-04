# Checkinn
Checking inn system
# 🌿 FarmTrack — Farm Work Management System

A production-grade, fully modular Single-Page Application for tracking
farm work hours, check-ins, and generating detailed reports.
Deployable to Vercel in under 2 minutes. No build step required.

---

## 🚀 Deploy to Vercel

### Option A — Vercel CLI (recommended)
```bash
npm i -g vercel
cd farmtrack
vercel
```

### Option B — Vercel Dashboard
1. Unzip the project folder
2. Go to https://vercel.com/new
3. Drag and drop the folder → **Deploy**

---

## 🔐 Default Admin Credentials
| Field    | Value |
|----------|-------|
| Username | `` |
| Password | `` |

> Admin can update username and password after first login via the profile.

---

## 📁 Architecture — Industry-Standard Modular Structure

```
farmtrack/
├── index.html                   ← Entry point only (no logic)
│
├── styles/
│   ├── tokens.css               ← Design tokens (CSS variables)
│   ├── base.css                 ← Reset + global styles + SPA routing
│   ├── components.css           ← Buttons, forms, cards, tables, modals…
│   ├── layout.css               ← Sidebar, topbar, grid system
│   ├── auth.css                 ← Login & register pages
│   └── dashboard.css            ← Dashboard-specific styles
│
├── store/
│   └── db.js                    ← Data layer (localStorage CRUD, isolated)
│
├── utils/
│   └── time.js                  ← Pure date/time helpers (no side effects)
│
├── services/
│   ├── auth.js                  ← Authentication business logic
│   ├── checkin.js               ← Check-in operations & paste parsing
│   └── reports.js               ← Report engine & analytics
│
├── components/
│   ├── toast.js                 ← Toast notification system
│   ├── modal.js                 ← Reusable modal component
│   ├── sidebar.js               ← Navigation sidebar component
│   ├── charts.js                ← Chart.js renderers
│   └── report-renderer.js       ← HTML + PDF report rendering
│
├── pages/
│   ├── login.js                 ← Login page controller
│   ├── register.js              ← Register page controller
│   ├── dashboard.js             ← User dashboard (live clock, week view)
│   ├── checkin.js               ← Self check-in + autocomplete
│   ├── reports.js               ← My personal reports
│   ├── checkin-others.js        ← Post arrivals / paste check-in
│   ├── admin-dashboard.js       ← Admin overview dashboard
│   ├── admin-pages-1.js         ← Admin: Users, Check-In Manager, Reports
│   └── admin-pages-2.js         ← Admin: Charts, Work Suggestions
│
├── router.js                    ← SPA router (auth guards, page rendering)
└── vercel.json                  ← Vercel deployment config
```

### Dependency Order (loaded bottom-up)
```
store → utils → services → components → pages → router
```
Each layer only depends on layers below it. Zero circular dependencies.

---

## ✅ Feature Checklist

### Authentication
- [x] Register with 3 names, unique work number, username, 4-digit PIN
- [x] PIN entry with individual digit boxes (paste-friendly)
- [x] Cached session — stays logged in on refresh
- [x] Admin sees admin dashboard; regular users see user dashboard
- [x] Route guards — unauthenticated users redirected to login

### Check-In (Self)
- [x] Farm name with autocomplete from all historical entries
- [x] "Use Current Time" button + manual time input
- [x] Multiple farms per day (merged, no duplicates)
- [x] Arrival locked if posted by someone else (admin can override)
- [x] This week's timeline shown on check-in page

### Check-In Others
- [x] Paste collection text → auto-parse day, farmers, workers
- [x] Multi-user arrival: `joseph/dan/felix` at one time
- [x] Locked arrivals shown; non-admin cannot override
- [x] Today's activity feed

### Reports
- [x] **Weekly**: Mon–Sat for any selected week
- [x] **Mid-Month**: 1st–15th of any month
- [x] **End-of-Month**: 1st–last day (handles 28/29/30/31-day months)
- [x] Post-midnight arrivals handled (00:00–05:59 = same shift)
- [x] Overtime calculated from 18:00 (6 PM)
- [x] Totals: days worked, total hours, total overtime
- [x] **PDF download** for every report (individual + admin full)

### Admin Features
- [x] Admin dashboard with live clock, check-in overview
- [x] All users table (filterable, click to view detail)
- [x] Manual check-in for any user on any date
- [x] Edit arrival time (admin override, clears lock)
- [x] Revoke check-in with confirmation
- [x] Paste collection text (admin)
- [x] All-users reports: Weekly, Mid-Month, End-Month, Custom Range
- [x] Charts: Days Worked, Overtime, Total Hours, Radar comparison
- [x] Individual 6-week trend line chart
- [x] Work suggestions ranked by fairness (days + OT equity)
- [x] Admin is also a regular user (can check in, see own reports)

---

## 📊 Business Rules

| Rule | Value |
|------|-------|
| Work day start | 08:00 |
| Work day end (standard) | 18:00 |
| Overtime trigger | After 18:00 |
| Post-midnight shift | 00:00–05:59 treated as same shift |
| Standard week | Monday – Saturday |
| Weekly target | 48 hours |
| Saturday overtime | Calculated same as any other day |

---

## 🛠 Tech Stack
- **Frontend**: Vanilla JS (ES6+), HTML5, CSS3
- **Data**: localStorage (no backend needed)
- **Charts**: Chart.js v4
- **PDF**: jsPDF v2.5
- **Design**: Samsung One UI design language
- **Deployment**: Vercel static hosting
- **Build step**: None required
