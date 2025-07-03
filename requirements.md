Here’s how to integrate the **Technical and Functional Requirements** for the **three key backend features** into your existing `README.md` file. Insert this new section after the **API Structure** section or just before the **Database Schema** section.

---

### 📋 Technical & Functional Requirements

This section provides detailed requirements for the core backend modules: **User Authentication**, **Property Management**, and **Booking System**.

---

#### 🔐 1. User Authentication

##### ✅ Functional Requirements

* Register users (guest or host) using email and password.
* Support OAuth login (Google, Facebook).
* Authenticate users via JWT tokens.
* Protect routes based on user roles.

##### 📌 API Endpoints

**POST `/api/register`**

```json
Request:
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "SecurePass123",
  "role": "guest"
}

Response:
{
  "message": "User registered successfully",
  "token": "<jwt_token>"
}
```

**Validations**:

* Email must be unique and valid.
* Password must be at least 8 characters.
* Role must be either `guest` or `host`.

---

**POST `/api/login`**

```json
Request:
{
  "email": "john@example.com",
  "password": "SecurePass123"
}

Response:
{
  "token": "<jwt_token>",
  "user": {
    "id": 1,
    "first_name": "John",
    "role": "guest"
  }
}
```

---

**POST `/api/oauth/google`**

```json
Request:
{
  "token_id": "<GoogleOAuthToken>"
}

Response: Same structure as /api/login
```

##### 🧪 Performance Criteria

* Token generation < 200ms.
* Rate limit login/registration (5 req/min/IP).
* OAuth response time < 500ms.

---

#### 🏠 2. Property Management

##### ✅ Functional Requirements

* Hosts can create, update, delete property listings.
* Listings must include title, price, location, amenities, availability.
* Guests can view and filter listings.

##### 📌 API Endpoints

**POST `/api/properties`**

```json
Request:
{
  "title": "Cozy Beach House",
  "description": "A beautiful beach house with Wi-Fi.",
  "location": "Miami, FL",
  "price": 150,
  "amenities": ["wifi", "pool", "parking"],
  "available_from": "2025-07-01",
  "available_to": "2025-08-30"
}

Response:
{
  "id": 101,
  "message": "Property created successfully"
}
```

**GET `/api/properties?location=miami&guests=2`**

* Returns filtered list of properties (with pagination).

**PUT `/api/properties/{id}`**

* Host can update their property.

**DELETE `/api/properties/{id}`**

* Host can delete their listing.

##### 🧪 Performance Criteria

* Filtered search must respond within 300ms.
* Maximum 50 results per page.
* Image uploads handled asynchronously.

---

#### 📅 3. Booking System

##### ✅ Functional Requirements

* Guests can book available properties.
* Prevent double-bookings with date validation.
* Bookings support statuses: `pending`, `confirmed`, `canceled`, `completed`.
* Both guests and hosts can cancel bookings.

##### 📌 API Endpoints

**POST `/api/bookings`**

```json
Request:
{
  "property_id": 101,
  "check_in": "2025-07-10",
  "check_out": "2025-07-15"
}

Response:
{
  "booking_id": 301,
  "status": "pending",
  "message": "Booking request submitted"
}
```

**GET `/api/bookings`**

* Returns the user's booking history.

**PATCH `/api/bookings/{id}/cancel`**

* Cancel a booking request (role-based logic applies).

##### 🧪 Performance Criteria

* Booking confirmation < 400ms.
* Concurrency-safe booking validation.
* Background task auto-cancels unpaid bookings after 30 minutes.

---

