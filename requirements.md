# Airbnb Clone – Backend Requirement Specifications

This document outlines the functional and technical requirements for three key backend features of the Airbnb Clone system:

- User Authentication
- Property Management
- Booking System

---

## 1. 🔐 User Authentication

### Functional Requirements
- Allow users to register as a guest or host.
- Allow users to log in and obtain a secure token.
- Validate credentials and return appropriate errors.

### API Endpoints

#### POST /api/auth/register
- **Request Body:**
```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "secure123",
  "role": "guest"
}
Validations:

Email must be unique.

Password must be at least 8 characters.

Response (201 Created):

json
Copy
Edit
{
  "message": "User registered successfully",
  "user_id": "uuid"
}
POST /api/auth/login
Request Body:

json
Copy
Edit
{
  "email": "john@example.com",
  "password": "secure123"
}
Response (200 OK):

json
Copy
Edit
{
  "token": "jwt_token",
  "user_id": "uuid",
  "role": "guest"
}

2. 🏡 Property Management
Functional Requirements
Hosts can create, update, or delete their properties.

Guests can view all available listings with filters.

API Endpoints
POST /api/properties
Headers: Authorization: Bearer <token>

Request Body:

json
Copy
Edit
{
  "name": "Ocean View Apartment",
  "description": "Spacious apartment with a sea view",
  "location": "Cape Coast",
  "price_per_night": 120.00
}
Validations:

Only hosts can create properties.

Price must be a positive number.

Response (201 Created):

json
Copy
Edit
{
  "property_id": "uuid",
  "message": "Property created successfully"
}
GET /api/properties
Query Params (optional): location, price_min, price_max

Response:

json
Copy
Edit
[
  {
    "property_id": "uuid",
    "name": "Ocean View Apartment",
    "location": "Cape Coast",
    "price_per_night": 120.00
  }
]


3. 📅 Booking System
Functional Requirements
Guests can book properties for a date range.

Bookings must not overlap existing ones.

Total cost is auto-calculated.

API Endpoints
POST /api/bookings
Headers: Authorization: Bearer <token>

Request Body:

json
Copy
Edit
{
  "property_id": "uuid",
  "start_date": "2025-08-01",
  "end_date": "2025-08-05"
}
Validations:

Dates must be in the future.

No booking conflicts for the same property.

Response (201 Created):

json
Copy
Edit
{
  "booking_id": "uuid",
  "total_price": 480.00,
  "status": "pending"
}
⚙️ Performance and Security
JWT used for authentication and role validation.

Input validation on all endpoints to prevent injection attacks.

Database queries optimized with indexed columns (e.g., user_id, property_id).

Booking availability checked with efficient SQL range overlap logic.

