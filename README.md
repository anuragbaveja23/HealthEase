*** Begin Patch
*** Update File: /Users/anuragbaveja/Desktop/prescripto-full-stack/README.md
@@
-## Prescripto — Full‑Stack Appointment Platform
-
-A monorepo with a Node.js/Express backend and two React apps: a user‑facing frontend and an admin dashboard. Features authentication (JWT), doctor listing and availability, appointment booking/cancellation, profile management, and payments via Stripe or Razorpay. Assets are stored on Cloudinary. Backend uses MongoDB.
-
-### Tech Stack
-- Backend: Node.js, Express, MongoDB (Mongoose), JWT, Multer, Cloudinary, Stripe, Razorpay, CORS, Dotenv
-- Frontend/Admin: React, Vite, React Router, Axios, React‑Toastify, Tailwind CSS
-
-### Monorepo Structure
-- `backend/` — Express API (`/api/user`, `/api/admin`, `/api/doctor`)
-- `frontend/` — User web app (books appointments, profile, etc.)
-- `admin/` — Admin dashboard (manage doctors, appointments, metrics)
-
-### Prerequisites
-- Node.js 18+ and npm
-- MongoDB (Atlas or local). Note: do not use `@` in the password per code comment
-- Cloudinary account (for image uploads)
-- Stripe and/or Razorpay accounts (optional if you won’t take payments)
-
-### Environment Variables
-
-Create a `.env` in `backend/`:
-
-```env
-# Server
-PORT=4000
-
-# Database
-MONGODB_URI=mongodb+srv://<username>:<password>@<cluster-host>
-
-# Auth
-JWT_SECRET=your_jwt_secret
-
-# Admin credentials (for admin login)
-ADMIN_EMAIL=admin@example.com
-ADMIN_PASSWORD=strong_password
-
-# Cloudinary
-CLOUDINARY_NAME=your_cloud_name
-CLOUDINARY_API_KEY=your_api_key
-CLOUDINARY_SECRET_KEY=your_secret
-
-# Payments (optional)
-STRIPE_SECRET_KEY=sk_test_...
-RAZORPAY_KEY_ID=rzp_test_...
-RAZORPAY_KEY_SECRET=your_razorpay_secret
-
-# Currency (used for Stripe/Razorpay)
-CURRENCY=INR
-```
-
-Create a `.env` in `frontend/` and `admin/`:
-
-```env
-VITE_BACKEND_URL=http://localhost:4000
-```
-
-### Install & Run (Development)
-Run each app in its own terminal from the repo root:
-
-```bash
-# 1) Backend API
-cd backend && npm install && npm run server
-
-# 2) Frontend (user app)
-cd ../frontend && npm install && npm run dev
-
-# 3) Admin (admin dashboard)
-cd ../admin && npm install && npm run dev
-```
-
-- Backend runs on `http://localhost:4000` by default
-- Vite dev servers typically run on `http://localhost:5173` (frontend) and `http://localhost:5174` (admin) if ports are available
-
-### Build (Production)
-
-```bash
-cd frontend && npm run build
-cd ../admin && npm run build
-```
-
-Start the backend in production mode:
-
-```bash
-cd backend && npm install && npm start
-```
-
-### API Overview (Base URL: `http://localhost:4000`)
-
-- `POST /api/user/register` — Register user
-- `POST /api/user/login` — Login user (returns `token`)
-- `GET /api/user/get-profile` — Get profile (header `token`)
-- `POST /api/user/update-profile` — Update profile (multipart `image`, header `token`)
-- `POST /api/user/book-appointment` — Book appointment (header `token`)
-- `GET /api/user/appointments` — List user appointments (header `token`)
-- `POST /api/user/cancel-appointment` — Cancel appointment (header `token`)
-- `POST /api/user/payment-razorpay` — Create Razorpay order (header `token`)
-- `POST /api/user/verifyRazorpay` — Verify Razorpay
-- `POST /api/user/payment-stripe` — Create Stripe Checkout Session (header `token`)
-- `POST /api/user/verifyStripe` — Verify Stripe result
-
-- `POST /api/doctor/login` — Login doctor (returns `dtoken`)
-- `GET /api/doctor/appointments` — Doctor appointments (header `dtoken`)
-- `POST /api/doctor/cancel-appointment` — Cancel appointment (header `dtoken`)
-- `POST /api/doctor/complete-appointment` — Mark completed (header `dtoken`)
-- `POST /api/doctor/change-availability` — Toggle availability (header `dtoken`)
-- `GET /api/doctor/dashboard` — Stats (header `dtoken`)
-- `GET /api/doctor/profile` — Profile (header `dtoken`)
-- `POST /api/doctor/update-profile` — Update profile (header `dtoken`)
-- `GET /api/doctor/list` — Public doctor list
-
-- `POST /api/admin/login` — Login admin (returns `atoken`)
-- `GET /api/admin/all-doctors` — All doctors (header `atoken`)
-- `POST /api/admin/change-availability` — Toggle doctor availability (header `atoken`)
-- `GET /api/admin/appointments` — All appointments (header `atoken`)
-- `POST /api/admin/cancel-appointment` — Cancel appointment (header `atoken`)
-- `GET /api/admin/dashboard` — Admin stats (header `atoken`)
-
-Notes:
-- Headers are read in lowercase on the server: `token`, `dtoken`, `atoken`.
-- Frontend/Admin store tokens in `localStorage` (`token` for users, `aToken` for admin). Axios will send headers you specify; Node will expose them lowercased in `req.headers`.
-
-### Payments
-- Set `CURRENCY` (e.g., `INR`). Razorpay uses it directly; Stripe uses a lowercase version internally.
-- If not using payments, you can omit Stripe/Razorpay keys and avoid calling those endpoints.
-
-### File Uploads
-- Profile and doctor images are uploaded to Cloudinary. Ensure Cloudinary env vars are set.
-
-### Troubleshooting
-- MongoDB connection string must not contain `@` in the password unless properly URL‑encoded; otherwise connection can fail (see comment in `backend/config/mongodb.js`).
-- If a Vite port is in use, Vite will prompt to use the next available port.
-
-### Documentation
-- See `How_To_Run_Project.pdf` in the repo root for additional run instructions.
+### Prescripto — Smart Healthcare Appointments
+
+Prescripto is a streamlined appointment platform that connects patients with the right doctors at the right time. It brings discovery, booking, payments, and basic care workflows into a single, simple experience for patients, doctors, and administrators.
+
+### The Problem
+- Finding the right specialist is slow and fragmented across multiple sites
+- Limited visibility into doctors’ real‑time availability causes back‑and‑forth and drop‑offs
+- Missed appointments and unclear payment flows reduce care efficiency and trust
+- Clinics lack a unified view of demand, revenue, and utilization
+
+### The Solution
+Prescripto centralizes the journey:
+- Verified doctor profiles with specialities, experience, fees, and availability
+- Real‑time slot booking and cancellations with instant feedback
+- Optional integrated payments for a smoother, faster checkout
+- Patient and doctor profiles to keep information accurate and up‑to‑date
+- Admin oversight for appointments, doctors, and high‑level metrics
+
+### Key Features
+- Browse specialities and view transparent fees and availability
+- Book, manage, and cancel appointments with clear confirmations
+- Seamless payments (Stripe or Razorpay) to reduce no‑shows
+- Doctor dashboard for earnings, appointment volume, and patient counts
+- Admin dashboard for platform‑wide visibility and control
+
+### Who It Serves & Value
+- Patients: faster discovery, confidence in choices, fewer no‑shows, predictable costs
+- Doctors: better scheduling, reduced admin work, improved utilization
+- Administrators: a single source of truth for operations and growth
+
+### Impact (Examples)
+- Higher booking completion rates through real‑time availability and simpler flows
+- Reduced no‑shows via pre‑payment and instant confirmations
+- Better clinic utilization with visibility into demand and performance
+
+### Future Scope
+- Teleconsultation and digital prescriptions
+- Insurance and claims integrations
+- Calendar sync and automated reminders
+- Analytics for capacity planning and patient outcomes
*** End Patch