# 🏥 Hospital Management API

This is a Django REST Framework-based backend system for a hospital application that supports:
- JWT authentication
- Patient registration and management
- Doctor directory (managed by admins)
- Role-based access control (patient, admin)
- CRUD operations for patients (with restricted access)
- Read-only access to doctors for public/patients

---

## 🚀 Features

- JWT-based authentication (`/api/auth/login`, `/api/auth/refresh/`)
- Patient self-registration endpoint (`/api/auth/register/`)
- Admin-managed doctor creation via admin panel or API
- Permissions:
  - Patients can manage only their own records
  - Admins can manage all patient and doctor records
  - Doctors are read-only for public and patients
- Cleanly structured with ModelViewSets and custom permissions

---

## 🛠️ Technologies Used

- Python 3.x
- Django 5.2
- Django REST Framework
- SimpleJWT (for authentication)
- SQLite (default, easily swappable with PostgreSQL)

---

## 📂 API Endpoints

| Method | Endpoint                 | Description                            | Auth Required |
|--------|--------------------------|----------------------------------------|---------------|
| POST   | `/api/auth/register/`    | Register as a patient                  | ❌            |
| POST   | `/api/auth/login/`       | Get JWT access & refresh tokens        | ❌            |
| POST   | `/api/auth/refresh/`     | Refresh JWT token                      | ❌            |
| GET    | `/api/doctors/`          | List all doctors (read-only)           | ❌            |
| POST   | `/api/doctors/`          | Create a doctor (admin only)           | ✅            |
| GET    | `/api/patients/`         | List all patients (admin only)         | ✅            |
| GET    | `/api/patients/{id}/`    | Retrieve a patient (self or admin)     | ✅            |
| PUT    | `/api/patients/{id}/`    | Update a patient (self or admin)       | ✅            |
| DELETE | `/api/patients/{id}/`    | Delete a patient (admin only)          | ✅            |

---

## 🔐 Roles & Permissions

| Role     | Can Register | View Doctors | Manage Doctors | Manage Patients |
|----------|--------------|--------------|----------------|------------------|
| Patient  | ✅           | ✅            | ❌              | Own Only          |
| Admin    | ❌           | ✅            | ✅              | All               |
| Anonymous| ❌           | ✅            | ❌              | ❌                |

