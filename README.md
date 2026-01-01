# Nice & Easy Gym – Full‑Stack Web App 💪🏽🚀

A friendly, practical app that turns “join a gym” into “start, learn, and keep going.” It welcomes newcomers, supports committed members, and helps coaches scale care. Inside you’ll find a production‑ready React + Vite frontend and an Express/MongoDB backend with payments, media, and admin tooling.

<img width="1892" height="1079" alt="image" src="https://github.com/user-attachments/assets/0029ffce-1b2b-4366-a6ff-636876348387" />


---

## Why This Exists (The Story) 📖
We wanted the gym experience to feel like a guided journey, not a guessing game. So we asked ourselves:
- What helps someone start without feeling lost? Clear courses, a friendly UI, and quick sign‑up.
- What keeps someone going? Measurable progress, structured lectures, and a checkout that “just works”.
- How do coaches scale care? Simple content tools, reliable media, and useful contact insights.

Our tech answers those questions without shouting about itself:
- React + Vite keep the app fast and fun to use.
- Tailwind + Bootstrap balance speed (utilities) with polish (components).
- JWT auth + bcrypt make security feel invisible but solid.
- Razorpay handles payments people trust.
- Cloudinary streams media smoothly so you don’t babysit servers.
- MongoDB models map to real gym life: `User`, `Courses`, `Lecture`, `Progress`, `Payment`, `Contact`.

---

## Highlights ✨
- Modern SPA with protected routes and admin dashboards.
- Course catalog with rich descriptions and smooth lecture streaming ▶️.
- Secure authentication, email OTP verification, and password reset 🔐.
- Seamless Razorpay checkout; per‑course purchase tracking 💳.
- Per‑user progress tracking across lectures 📈.
- Media upload + hosting on Cloudinary (images/videos) ☁️.
- Contact intake saved and emailed to your inbox 📬.

---

## Architecture 🏗️
- Frontend: React 18 + Vite 5, TailwindCSS, Bootstrap, React Router.
- Backend: Node.js (Express), MongoDB (Mongoose), JWT auth, Razorpay, Nodemailer, Cloudinary.
- Boundary: REST API under `/api` mounted by the backend.
- Deployment: Stateless frontend, stateful backend with env‑driven config and managed media.

Folder map:
- Frontend app: [frontend/src](frontend/src)
- Backend entry: [server/index.js](server/index.js)
- Routes: [server/routes](server/routes)
- Controllers: [server/controllers](server/controllers)
- Models: [server/models](server/models)
- Middlewares: [server/middlewares](server/middlewares)

## File Structure 🗂️
Here’s a quick tour so you can get your bearings fast:

```
Gym-website-final/
├─ frontend/
│  ├─ src/
│  │  ├─ pages/           # Home, Auth, Courses, Study, Admin
│  │  ├─ components/      # UI blocks (header, footer, cards, etc.)
│  │  ├─ admin/           # Admin dashboard, courses, users
│  │  ├─ context/         # User/Course context providers
│  │  ├─ App.jsx          # Routes + layout
│  │  └─ main.jsx         # App bootstrap + base URL
│  ├─ public/
│  ├─ index.css           # Tailwind entry
│  ├─ vite.config.js
│  └─ package.json
└─ server/
  ├─ index.js            # Express app + routes mount
  ├─ database/db.js      # Mongo connection
  ├─ routes/             # user.js, course.js, admin.js
  ├─ controllers/        # user, course, admin, contact
  ├─ models/             # User, Courses, Lecture, Payment, Progress, Contact
  ├─ middlewares/        # isAuth, multer, sendMail, TryCatch
  └─ package.json
```

---

## Tech Choices Per Feature 🧠
- Authentication: JWT via [isAuth](server/middlewares/isAuth.js) + bcrypt; OTP email with Nodemailer. Goal: secure yet easy logins and smooth resets.
- Courses & Lectures: Mongoose schemas ([Courses](server/models/Courses.js), [Lecture](server/models/Lecture.js)); Cloudinary for heavy media. Goal: simple authoring, reliable playback.
- Payments: Razorpay in the [course controller](server/controllers/course.js) with signature verification and [Payment](server/models/Payment.js) audit. Goal: trust and traceability.
- Progress: [Progress](server/models/Progress.js) marks completed lectures. Goal: visible momentum that keeps people coming back.
- Admin Tools: [isAdmin](server/middlewares/isAuth.js) gates create/edit/delete, role toggles, stats, and contact intake. Goal: control without complexity.
- Contact & Engagement: [Contact](server/models/Contact.js) saves rich intake; [sendContactMail](server/middlewares/sendMail.js) forwards details. Goal: fast follow‑ups.

---

## Features 🎯
- Account
  - Register with OTP verification ✉️
  - Login/logout and secure route protection 🔒
  - Forgot/Reset password via signed tokens 🔁
- Catalog & Study
  - Course listing, detailed pages, and lecture playback ▶️
  - Access gating by subscription; purchase history 📚
  - My Courses view and progress percentage 📊
- Payments
  - Razorpay order creation and signature verification ✅
  - Purchase persistence and course popularity tracking 🔥
- Admin
  - Create/edit/delete courses with image/video uploads 📤
  - Add/delete lectures with Cloudinary streaming 🎞️
  - View stats (courses, lectures, users), toggle roles 🧮
  - See contact submissions 📨
- Communication
  - Contact intake stored and forwarded by email 📬

---

## API Overview 🔌
Base URL: `http://localhost:5000/api`

User:
- POST `/user/register`, `/user/verify`, `/user/login`
- GET `/user/me` (JWT)
- POST `/user/forgot`, `/user/reset`
- POST `/user/progress` (JWT), GET `/user/progress` (JWT)
- POST `/user/sendContactMail`
- POST `/user/contact`

Course:
- GET `/course/all`, `/course/:id`
- GET `/lectures/:id` (JWT), `/lecture/:id` (JWT)
- GET `/mycourse` (JWT)
- POST `/course/checkout/:id` (JWT)
- POST `/verification/:id` (JWT)
- GET `/courses/popular`

Admin (JWT + admin):
- POST `/course/new` (image upload)
- POST `/course/:id` (video upload)
- PUT `/course/:id`
- DELETE `/course/:id`, `/lecture/:id`
- GET `/stats`, `/users`, `/course/:id`
- GET `/contact`

See route definitions in [server/routes/user.js](server/routes/user.js#L24), [server/routes/course.js](server/routes/course.js#L1), and [server/routes/admin.js](server/routes/admin.js#L63).

---

## Data Models 🧩
- Users: [server/models/User.js](server/models/User.js#L1)
- Courses: [server/models/Courses.js](server/models/Courses.js#L1)
- Lectures: [server/models/Lecture.js](server/models/Lecture.js#L1)
- Progress: [server/models/Progress.js](server/models/Progress.js#L1)
- Payment: [server/models/Payment.js](server/models/Payment.js#L1)
- Contact: [server/models/Contact.js](server/models/Contact.js#L1)

---

## Setup (Windows) 🪟
Prerequisites:
- Node.js 18+
- MongoDB Atlas (or local MongoDB) connection string
- Razorpay keys
- Cloudinary account
- Gmail SMTP (App Password) for emails

1) Configure backend env: create `server/.env` with:
```
PORT=5000
DB=mongodb+srv://<user>:<pass>@<cluster>/<db>?retryWrites=true&w=majority
Jwt_Sec=your_jwt_secret
Activation_Secret=your_activation_secret
Forgot_Secret=your_forgot_secret
Razorpay_Key=rzp_test_xxx
Razorpay_Secret=xxxxxx
Gmail=your@gmail.com
Password=your_app_password
frontendurl=http://localhost:5173
CLOUDINARY_CLOUD_NAME=xxxx
CLOUDINARY_API_KEY=xxxx
CLOUDINARY_API_SECRET=xxxx
ContactEmail=leads@yourdomain.com
```

2) Install and run:
```powershell
cd server
npm install
npm run start
```
In a new terminal:
```powershell
cd frontend
npm install
npm run dev
```

3) Open the app:
- Frontend dev server: http://localhost:5173
- Backend server: http://localhost:5000

Notes:
- The frontend base URL is set in [frontend/src/main.jsx](frontend/src/main.jsx#L7). Adjust for production.
- JWT is read from `localStorage` and sent as `headers.token`.

---

## Security & Privacy 🔐
- Auth: JWT with short‑lived tokens by design; refresh flow can be added.
- Passwords: Hashed with bcrypt; never stored in plain text.
- Payments: Razorpay signature verification on server.
- Media: Cloudinary public URLs; admin‑only upload/delete.
- Email: SMTP via Gmail; use app passwords; avoid plain credentials.

---

## Frontend Notes 🧭
- Router guards ensure only authenticated users hit study/admin routes.
- UI stack: Tailwind utilities for speed, Bootstrap for components where useful.
- Notifications: react‑hot‑toast for friendly feedback.
- Video: Cloudinary video URLs rendered via player components.

Key files:
- App routes: [frontend/src/App.jsx](frontend/src/App.jsx#L1)
- User context: [frontend/src/context/UserContext.jsx](frontend/src/context/UserContext.jsx#L1)
- Course context: [frontend/src/context/CourseContext.jsx](frontend/src/context/CourseContext.jsx)

---

## Backend Notes 🛠️
- Entry & mount: [server/index.js](server/index.js#L1)
- DB connect: [server/database/db.js](server/database/db.js#L1)
- Auth middleware: [server/middlewares/isAuth.js](server/middlewares/isAuth.js#L1)
- File uploads: [server/middlewares/multer.js](server/middlewares/multer.js#L1)
- Mailers: [server/middlewares/sendMail.js](server/middlewares/sendMail.js#L1)
- Controllers: [server/controllers](server/controllers)

---

## Performance & Reliability ⚡
- Vite + React keeps dev and prod builds fast.
- Cloudinary offloads media delivery at scale.
- Razorpay orders/signatures avoid payment drift.
- Mongoose indexes can be added on hot fields (e.g., `email`).

---

## Accessibility & UX ♿
- Clear affordances for courses, progress, and checkout.
- Toasts and statuses for async actions.
- Can be extended with ARIA roles and keyboard navigation.

---

## Roadmap 🗺️
- Add refresh tokens + role‑based UI controls.
- Lecture transcripts and captions.
- Rate limiting + IP throttling.
- Admin analytics dashboards.
- E2E tests (Playwright) + API tests.

---

## FAQ ❓
- Payments fail — what happens?
  - Server rejects non‑matching signatures and leaves subscriptions unchanged.
- Why both Tailwind and Bootstrap?
  - Utility speed plus component clarity — used where each fits best.
- Can local media be used?
  - Yes, but Cloudinary reduces ops work and scales better.

---

## Contributing 🤝
- Fork, create a feature branch, commit with clear messages, open a PR.
- Please avoid including secrets; use `.env`.
