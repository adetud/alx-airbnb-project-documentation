# Airbnb Clone Backend - Requirement Specifications

This document outlines the technical and functional specifications for key backend features of the Airbnb Clone project.

---

## 1️⃣ User Authentication

### Description
Handles user registration, login, and authentication using secure credentials.

### API Endpoints
| Method | Endpoint | Description |
|--------|-----------|--------------|
| POST | /api/register | Register a new user |
| POST | /api/login | Authenticate and log in a user |
| GET | /api/users/:id | Fetch a user profile |

### Input / Output
**Input (POST /api/register):**
```json
{
  "name": "Daniel Adetu",
  "email": "daniel@example.com",
  "password": "securePassword123"
}
Output (Success):

json
Copy code
{
  "message": "User created successfully",
  "user_id": 1
}
Validation
Email must be unique and valid.

Password must be at least 8 characters.

All fields required.

Security
Passwords hashed using bcrypt.

Authentication tokens handled with JWT.

2️⃣ Property Management
Description
Allows hosts to create, update, and delete property listings.

API Endpoints
Method	Endpoint	Description
POST	/api/properties	Add a new property
PUT	/api/properties/:id	Update property details
DELETE	/api/properties/:id	Delete a property
GET	/api/properties	View all available properties

Input / Output
Input (POST /api/properties):

json
Copy code
{
  "host_id": 1,
  "title": "Modern Apartment in Lagos",
  "price": 50000,
  "location": "Lekki Phase 1"
}
Output:

json
Copy code
{
  "message": "Property created successfully",
  "property_id": 10
}
Validation
Title, price, and location required.

Price must be a positive number.

Performance
Indexed columns: price, location

Caching property list responses to improve speed.

3️⃣ Booking System
Description
Enables users to book properties and manage reservations.

API Endpoints
Method	Endpoint	Description
POST	/api/bookings	Create a booking
GET	/api/bookings/:id	View a specific booking
GET	/api/bookings	List all bookings for a user
DELETE	/api/bookings/:id	Cancel a booking

Input / Output
Input (POST /api/bookings):

json
Copy code
{
  "user_id": 2,
  "property_id": 10,
  "check_in": "2025-11-05",
  "check_out": "2025-11-10"
}
Output:

json
Copy code
{
  "message": "Booking successful",
  "booking_id": 100
}
Validation
Dates must be valid (check-out after check-in).

Property must be available during requested dates.

Security
Booking endpoints require authentication.

Cross-check with property ownership to prevent fake bookings.

