# Dental Clinic Management System

Full-stack clinic management system with JWT auth, RBAC, doctor management, appointments, patient medical history, audit logs, and dashboard analytics.

## Tech Stack

- Frontend: React + Tailwind CSS + React Router + Axios
- Backend: Node.js + Express
- Database: MySQL + Sequelize ORM
- Authentication: JWT access token + refresh token rotation (HTTP-only cookie)

## Features

- Register/login with bcrypt password hashing
- JWT access + refresh token rotation
- RBAC roles: `admin`, `doctor`, `staff`
- Doctor CRUD (admin)
- Patient CRUD (admin)
- Patient History CRUD (admin + doctor with doctor-level restriction)
- Appointment CRUD (admin + staff), linked to both patient and doctor
- Dashboard charts:
  - patients per doctor
  - appointments per month
  - appointments by status
- Audit logs for auth and CRUD actions
- React dashboard with role-based navigation
- Form validation on backend (Joi)

## Project Structure

```text
clinic-app/
  backend/
    src/
      config/
      controllers/
      middleware/
      models/
      routes/
      seeders/
      utils/
      app.js
      server.js
  frontend/
    src/
      api/
      components/
      context/
      pages/
      utils/
```

## Backend Setup

1. Go to backend:
   - `cd backend`
2. Install dependencies:
   - `npm install`
3. Create `.env` from `.env.example`
4. Create MySQL database matching `DB_NAME`
5. Run migrations:
   - `npm run migrate`
6. Run seed data:
   - `npm run seed`
7. Start backend:
   - `npm run dev`

Default seeded accounts:
- Admin: `admin@clinic.com / Admin@123`
- Doctor: `doctor@clinic.com / Doctor@123`
- Staff: `staff@clinic.com / Staff@123`

## Frontend Setup

1. Go to frontend:
   - `cd frontend`
2. Install dependencies:
   - `npm install`
3. Create `.env` from `.env.example`
4. Start frontend:
   - `npm run dev`

Frontend runs on `http://localhost:5173` and backend on `http://localhost:5000`.

## API Endpoints

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/refresh-token`
- `POST /api/auth/logout`

### Dashboard
- `GET /api/dashboard/overview` (protected)
- `GET /api/dashboard/analytics` (protected)

### Doctors
- `GET /api/doctors` (admin, doctor, staff)
- `POST /api/doctors` (admin)
- `PUT /api/doctors/:id` (admin)
- `DELETE /api/doctors/:id` (admin)

### Patients
- `POST /api/patients` (protected)
- `GET /api/patients` (protected)
- `PUT /api/patients/:id` (protected)
- `DELETE /api/patients/:id` (protected)

### Appointments
- `POST /api/appointments` (protected)
- `GET /api/appointments` (protected)
- `PUT /api/appointments/:id` (protected)
- `DELETE /api/appointments/:id` (protected)

### Patient History
- `POST /api/patient-history` (admin, doctor)
- `GET /api/patient-history` (admin, doctor)
- `PUT /api/patient-history/:id` (admin, doctor)
- `DELETE /api/patient-history/:id` (admin, doctor)

### Audit Logs
- `GET /api/audit-logs` (admin)

## Security Notes

- Passwords are hashed with bcrypt
- Access tokens are short-lived
- Refresh tokens:
  - sent via HTTP-only cookie
  - stored hashed in DB
  - rotated on refresh
- Role-based endpoint protection using JWT payload role
- CRUD/login/logout actions logged into `audit_logs`

## Next Improvements

- Add automated tests (unit + integration)
- Add calendar/scheduler UI
- Add advanced report export
