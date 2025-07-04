# Requirements Specification Document

## Project: Airbnb Clone (Backend)

---

## 1. ✨ User Authentication

### 📌 Overview
The system must allow users to register, log in, and manage their accounts securely.

### 🚀 Functional Requirements
- Users can **register** using email, password, first name, and last name.
- Users can **log in** using email and password.
- Passwords must be stored securely (**hashed**).
- Users can **update** or **delete** their profile.

### 🔗 API Endpoints

| Method | Endpoint            | Description                |
|--------|---------------------|----------------------------|
| POST   | `/api/register`      | Register a new user        |
| POST   | `/api/login`         | Authenticate existing user |
| GET    | `/api/user/profile`  | Get user profile           |
| PUT    | `/api/user/profile`  | Update user profile        |
| DELETE | `/api/user/profile`  | Delete user profile        |

### 📝 Input/Output

- **Registration Input:**  
  `email`, `password`, `first_name`, `last_name`

- **Login Input:**  
  `email`, `password`

- **Output:**  
  JWT token, success/failure message

### ✅ Validation Rules

- Email must be valid format and unique.
- Password must be **minimum 8 characters**.
- All fields are **required** during registration.

### ⚙️ Performance Criteria

- Responses within **500ms** under normal load.
- **Rate limiting** to prevent brute-force attacks.

---

## 2. 🏠 Property Management

### 📌 Overview
Hosts can list properties, update details, or remove listings.

### 🚀 Functional Requirements
- Hosts can **create**, **read**, **update**, and **delete** property listings.
- Properties must have:
  - Name
  - Description
  - Location
  - Price per night
  - Availability status

### 🔗 API Endpoints

| Method | Endpoint              | Description                   |
|--------|-----------------------|-------------------------------|
| POST   | `/api/properties`      | Create a new property listing |
| GET    | `/api/properties`      | Get list of all properties    |
| GET    | `/api/properties/:id`  | Get details of a property     |
| PUT    | `/api/properties/:id`  | Update property               |
| DELETE | `/api/properties/:id`  | Delete property               |

### 📝 Input/Output

- **Input:**  
  `name`, `description`, `location`, `pricePerNight`, `images`, `status`

- **Output:**  
  property ID, full details, success/failure

### ✅ Validation Rules

- Price must be a **positive number**.
- Name, description, and location are **mandatory**.
- Only authenticated **hosts** can manage properties.

### ⚙️ Performance Criteria

- Support for **concurrent access**.
- Use **pagination** for property lists.

---

## 3. 📅 Booking System

### 📌 Overview
Users can book properties for available dates.

### 🚀 Functional Requirements
- Users can **create**, **view**, or **cancel** bookings.
- Check **property availability** before booking.
- **Total price** is calculated based on the stay duration.

### 🔗 API Endpoints

| Method | Endpoint            | Description             |
|--------|---------------------|-------------------------|
| POST   | `/api/bookings`      | Create new booking      |
| GET    | `/api/bookings`      | View all bookings       |
| DELETE | `/api/bookings/:id`  | Cancel a booking        |

### 📝 Input/Output

- **Input:**  
  `property_id`, `start_date`, `end_date`, payment info

- **Output:**  
  booking ID, status, total price

### ✅ Validation Rules

- Booking dates must **not overlap** with existing bookings.
- Start date must be **before** end date.
- Only **authenticated users** can book.

### ⚙️ Performance Criteria

- Booking confirmation within **1 second**.
- Handle **concurrent booking requests** safely.

---

