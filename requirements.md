# Backend Requirement Specifications for Airbnb Clone
This document details some backend requirement specifications for the Airbnb clone project.

## 1. User Authentication
This system manages user registration, authentication, and profile maintenance for both Guests and Hosts.

### Endpoints

* **POST /api/v1/users/register** - Creates a new user account.
* **POST /api/v1/users/login** - Authenticates user and returns JWT token.
* **GET /api/v1/users/{userId}** - Retrieves specific user profile

### Validations

* **Email:** Must be valid and unique.
* **Password:** Minimum length of 8 characters and hashed using bcrypt.
* **User ID (userId):** Must be a valid UUID.

## Response
Upon successful user authentication, the system returns:
* JSON containing `success message`, `jwt_token`, `userId`, and `role`.

---

## 2. Listing Management
This system allows Hosts to create, view, update, and delete property listings available for booking.

### Endpoints

* **POST /api/v1/listings** - Creates a new listing.
* **GET /api/v1/listings/{listingId}** - Retrieves a single listing.
* **PUT /api/v1/listings/{listingId}** - Updates an existing listing.
* **DELETE /api/v1/listings/{listingId}** - Deletes a listing.

### Validations

* **Price per Night:** Must be an integer greater than or equal to 1.
* **Max Guests:** Must be an integer greater than 0.
* **Title:** Minimum length of 5 characters.

## Response
* JSON content including `host_id`, `rating`, `review_count`, `title`, `description`, `price_per_night`, `max_guests`, `location`, and `amenities`.

---

## 3. Booking Management
This system handles the reservation process, managing availability and guest bookings against property listings.

### Endpoints

* **POST /api/v1/bookings** - Creates a new booking.
* **GET /api/v1/users/{userId}/bookings** - Retrieves all bookings for a user.
* **DELETE /api/v1/bookings/{bookingId}** - Cancels an existing booking.

### Validations

* **Dates:** check_out_date must be after check_in_date. Both dates must be in the future (or today for check-in).
* **Availability:** The system must check that the requested dates do not conflict with any existing, confirmed bookings for the listing_id.
* **Guest Count:** num_guests must not exceed the max_guests capacity of the listing.

## Response
Upon successful booking, the system returns:
* JSON containing `success message`, `booking_id`, `total_price`, and `status`.

---

## Non-Functional Requirements (NFRs)
* **Performance:** Focuses on speed and response time, primarily concerned with user experience.
* **Security:** Focuses on protecting data and systems. Robust token generation and password hashing.
* **Reliability:** Focuses on consistency, availability, and error prevention (e.g., ensuring a database transaction is fully completed or completely undone).
* **Scalability:** The low latency requirements (Performance) and transactional guarantees (Reliability) are crucial foundations for building a system that can scale later on.
