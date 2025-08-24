# airbnb-clone-project

## 🏠 Project Overview

### 📌 Description

This project is a **web-based Airbnb clone** that allows users to list, browse, and book short-term rental properties. The platform is designed to support both **guests** and **hosts**, featuring functionalities such as user authentication, property listings, availability calendars, booking management, and secure payments.

### 🎯 Project Goals

* Build a scalable and responsive web application for booking accommodations.
* Enable users to register, list properties, and manage bookings with ease.
* Ensure seamless integration between frontend and backend using RESTful APIs.
* Implement a secure and user-friendly interface for both hosts and travelers.
* Follow best practices in software architecture, testing, and deployment.

### 🧰 Tech Stack

**Frontend:**

* **Vue.js** – JavaScript framework for building the interactive user interface.
* **Vue Router** – Handles client-side routing.
* **Axios** – For making API requests to the Django backend.
* **Tailwind CSS / Bootstrap (optional)** – For fast and responsive UI design.

**Backend:**

* **Django** – High-level Python web framework for server-side logic.
* **Django REST Framework (DRF)** – For building RESTful APIs consumed by the frontend.
* **PostgreSQL** – Relational database for storing user data, listings, bookings, etc.
* **Celery + Redis** – For handling asynchronous tasks such as email notifications (optional).
* **Stripe or PayPal API** – For handling secure payments (optional).

**DevOps & Deployment:**

* **Docker** – Containerization for development and deployment.
* **Nginx + Gunicorn** – Web server and application server stack.
* **GitHub Actions / GitLab CI** – CI/CD pipelines for automated testing and deployment.
* **AWS / DigitalOcean / Heroku** – Cloud platforms for deployment.

## 🗃️ Database Design

The database schema is designed to support all core Airbnb-like features including user management, property listings, bookings, payments, and reviews. Below are the key entities, their fields, and how they relate to one another.

### 🧑 Users

Represents both guests and hosts on the platform.

**Key Fields:**

* `id` (Primary Key)
* `username` – Unique user identifier
* `email` – For communication and login
* `password_hash` – Securely stored password
* `is_host` – Boolean indicating if the user can list properties

**Relationships:**

* A user **can create** multiple properties (if a host).
* A user **can make** multiple bookings (if a guest).
* A user **can leave** multiple reviews.

---

### 🏘️ Properties

Represents accommodations listed by hosts.

**Key Fields:**

* `id` (Primary Key)
* `host` (Foreign Key → Users)
* `title` – Name of the listing
* `description` – Detailed info about the property
* `location` – Address or coordinates

**Relationships:**

* A property **belongs to** one host.
* A property **can have** multiple bookings.
* A property **can receive** multiple reviews.

---

### 📅 Bookings

Handles reservation information for guests.

**Key Fields:**

* `id` (Primary Key)
* `property` (Foreign Key → Properties)
* `guest` (Foreign Key → Users)
* `check_in` – Start date of booking
* `check_out` – End date of booking
* `status` – Confirmed, canceled, pending, etc.

**Relationships:**

* A booking **is made by** one user (guest).
* A booking **is linked to** one property.
* A booking **can be linked to** one payment.

---

### 💳 Payments

Tracks financial transactions related to bookings.

**Key Fields:**

* `id` (Primary Key)
* `booking` (Foreign Key → Bookings)
* `amount` – Total payment amount
* `status` – Paid, failed, pending
* `payment_method` – e.g., Stripe, PayPal

**Relationships:**

* A payment **belongs to** one booking.

---

### ⭐ Reviews

Allows users to provide feedback on properties.

**Key Fields:**

* `id` (Primary Key)
* `property` (Foreign Key → Properties)
* `author` (Foreign Key → Users)
* `rating` – Score (e.g., 1 to 5)
* `comment` – Text review
* `created_at` – Timestamp

**Relationships:**

* A review **is written by** one user.
* A review **is about** one property.

---

### 🔗 Entity Relationship Summary

```plaintext
User ────────┐
    ▲        │
    │        ▼
 Reviews   Properties ◄────────── User (Host)
    ▲          │
    │          ▼
  Bookings ◄───┘
    │
    ▼
 Payments
```

## 🧑‍💻 Team Roles

Below are the key roles involved in developing this Airbnb-style application using Django and Vue.js:

### 🔧 Backend Developer (Django)

**Responsibilities:**

* Develops the server-side logic using Django.
* Implements RESTful APIs for frontend integration.
* Manages user authentication, listing creation, booking logic, and payment processing.
* Ensures scalability and performance of the backend system.

### 🎨 Frontend Developer (Vue.js)

**Responsibilities:**

* Builds a responsive and interactive user interface using Vue.js.
* Connects with backend APIs to display data dynamically.
* Implements client-side logic such as routing, state management, and form validation.
* Ensures a smooth and intuitive user experience.

### 🛢️ Database Administrator (DBA)

**Responsibilities:**

* Designs and manages the database schema using PostgreSQL or another RDBMS.
* Ensures data integrity, indexing, and performance tuning.
* Sets up regular backups and manages migrations.
* Works closely with the backend team to optimize queries.

### 🧪 QA Engineer

**Responsibilities:**

* Writes and executes test cases for both frontend and backend.
* Performs manual and automated testing of features like search, booking, and payments.
* Reports and tracks bugs, ensuring issues are resolved before deployment.
* Validates UI/UX consistency across browsers and devices.

### 🎯 Project Manager

**Responsibilities:**

* Oversees the project timeline, scope, and deliverables.
* Coordinates between team members and ensures effective communication.
* Tracks progress using tools like Jira or Trello.
* Manages stakeholder expectations and organizes sprint reviews.

### 🎨 UI/UX Designer

**Responsibilities:**

* Designs wireframes, mockups, and high-fidelity UI screens.
* Defines the overall look and feel of the application.
* Conducts user research and usability testing.
* Collaborates with developers to ensure design feasibility.

### 🔐 DevOps Engineer

**Responsibilities:**

* Sets up and manages CI/CD pipelines.
* Automates deployment processes for both frontend and backend.
* Monitors application health and server uptime.
* Ensures secure and scalable cloud infrastructure (e.g., AWS, Azure, or Docker/Kubernetes).
