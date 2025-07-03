# 🏡 Airbnb Clone – Backend

Welcome to the backend of the **Airbnb Clone** project. This service powers core functionalities of a rental marketplace app, including user management, property listings, bookings, payments, and reviews.

---

## 📚 Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [Features](#features)
- [API Structure](#api-structure)
- [Database Schema](#database-schema)
- [Authentication & Authorization](#authentication--authorization)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Error Handling](#error-handling)
- [Testing](#testing)
- [License](#license)

---

## 📘 Project Overview

This is a full-featured backend built for an Airbnb-style booking platform. It supports secure user authentication, dynamic property listing management, booking logic with date validation, payment processing, and real-time notifications.

---

## 🛠️ Tech Stack

- **Language**: Python 3.x / Node.js (Choose based on your implementation)
- **Framework**: Django REST Framework / Express.js
- **Database**: PostgreSQL / MySQL
- **Authentication**: JWT (JSON Web Tokens)
- **Caching**: Redis (for performance)
- **File Storage**: Local / AWS S3 / Cloudinary
- **Email**: SendGrid / Mailgun
- **Payment Gateway**: Stripe / PayPal

---

## 🚀 Features

### 👤 User Management
- User registration (guest or host)
- Secure login (email/password, OAuth optional)
- Profile update with photo and preferences

### 🏠 Property Listings
- Hosts can add, edit, delete listings
- Fields: title, description, location, price, amenities, availability

### 🔍 Search & Filtering
- Search by location, price, guests, amenities
- Pagination for large result sets

### 📅 Booking Management
- Guests book available properties
- Date validation prevents double bookings
- Booking statuses: pending, confirmed, canceled, completed

### 💳 Payment Integration
- Guest payments via Stripe or PayPal
- Host payouts after completion
- Multi-currency support

### ⭐ Reviews & Ratings
- Guests can review booked properties
- Hosts can respond to reviews
- Reviews tied to valid bookings

### 🔔 Notifications
- Email and in-app for confirmations, cancellations, payments

### 🛠 Admin Dashboard
- Admins can manage users, listings, bookings, and payments

---

## 🔗 API Structure

Follows RESTful principles with proper HTTP verbs and status codes.

| Method | Endpoint                 | Description                 |
|--------|--------------------------|-----------------------------|
| POST   | /api/register            | Register user               |
| POST   | /api/login               | Login user                  |
| GET    | /api/properties          | List all properties         |
| POST   | /api/properties          | Create new property (host)  |
| POST   | /api/bookings            | Create new booking          |
| POST   | /api/payments/checkout   | Initiate payment            |
| GET    | /api/notifications       | Get user notifications      |

More endpoints documented via Swagger/Postman.

---

## 🗃️ Database Schema (Simplified)

- **Users**: `id`, `email`, `password_hash`, `role`, `profile_pic`, etc.
- **Properties**: `id`, `host_id`, `title`, `description`, `price`, etc.
- **Bookings**: `id`, `user_id`, `property_id`, `status`, `check_in`, `check_out`
- **Payments**: `id`, `booking_id`, `amount`, `currency`, `status`
- **Reviews**: `id`, `user_id`, `property_id`, `rating`, `comment`

---

## 🔐 Authentication & Authorization

- **JWT** used for session management
- **RBAC (Role-Based Access Control)**:
  - **Guest**: can search, book, review
  - **Host**: can manage listings
  - **Admin**: full access to all resources

---

## ⚙️ Installation

```bash
# Clone the project
git clone https://github.com/yourusername/airbnb-clone-backend.git
cd airbnb-clone-backend

# Install dependencies
pip install -r requirements.txt  # or npm install

# Setup database
python manage.py migrate

# Run the server
python manage.py runserver
