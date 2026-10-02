<p align="center">
  <h1 align="center">Hotel Management System</h1>
</p>

<p align="center">
  A Laravel REST API for managing hotel operations, bookings, rooms, staff, shifts, tasks, and guest service requests.
</p>

<p align="center">
  <a href="https://github.com/esraaghneem/hotel-management">
    <img src="https://img.shields.io/badge/Backend-Laravel%2012-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Laravel">
  </a>
  <img src="https://img.shields.io/badge/PHP-8.2%2B-777BB4?style=for-the-badge&logo=php&logoColor=white" alt="PHP">
  <img src="https://img.shields.io/badge/Database-MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge/Auth-Laravel%20Sanctum-FF2D20?style=for-the-badge&logo=laravel&logoColor=white" alt="Sanctum">
  <img src="https://img.shields.io/badge/API-RESTful-02569B?style=for-the-badge" alt="REST API">
</p>

<p align="center">
  <a href="https://github.com/esraaghneem/hotel-management">
    <strong>GitHub Repository</strong>
  </a>
  &nbsp; • &nbsp;
  <a href="https://hotel-management-system-production-97bb.up.railway.app">
    <strong>Live API</strong>
  </a>
</p>

---

## 🏨 About the Project

**Hotel Management System** is a backend-focused hotel management application built with **Laravel 12** and **MySQL**.

The system provides a RESTful API that supports hotel operations through separate customer and staff workflows.

The backend manages:

- Customer authentication
- Hotel room management
- Room bookings
- Staff management
- Staff roles and departments
- Shifts
- Tasks and task assignment
- Guest service requests
- Fixed task templates
- Role-based access control
- Protected API endpoints
- Staff availability and workload rules

The project was designed with a focus on clean architecture, separation of responsibilities, secure authentication, validation, and maintainable business logic.

---

## 🎯 System Architecture

The application is organized around three main areas:

    Hotel Management System
              |
       +------+------+
       |             |
    Customer       Staff
     System        System
       |             |
   +---+---+    +----+---------+
   |       |    |              |
Customers Bookings Management Operations
                 |              |
             Staff/Roles     Tasks
             Departments        |
                           Service Requests

---

## 🛠️ Technology Stack

### Backend

- PHP
- Laravel 12
- MySQL
- Laravel Sanctum
- Eloquent ORM
- RESTful API
- Form Requests
- API Resources
- Service Layer architecture

### Development & Testing

- Visual Studio Code
- PowerShell
- Postman
- phpMyAdmin
- Git
- GitHub

### Deployment

- Railway

---

## ✨ Main Features

### 👤 Customer Management

The customer side supports:

- Customer registration
- Customer authentication
- Customer login/logout
- Customer profile access
- Room browsing
- Room booking
- Booking management
- Guest service requests

Customer records use `customer_id` as the primary key.

---

### 🛏️ Room Management

The system provides room management functionality including:

- Creating rooms
- Viewing rooms
- Updating rooms
- Deleting rooms
- Room number validation
- Room image handling
- Room availability management
- Protected room modification operations

Room updates support partial field updates and validate room number uniqueness.

---

### 📅 Booking Management

Bookings are connected to customers and rooms and are used as the foundation for hotel operations.

The system validates booking-related operations before allowing dependent actions such as guest service requests.

Service requests require the customer to have an active booking.

---

### 👨‍💼 Staff Management

The system supports hotel staff management through protected API endpoints.

Staff records include information such as:

- Name
- Email
- Phone
- Password
- Department
- Role
- Active status
- Profile image

Staff management includes:

- Creating staff
- Updating staff roles
- Activating/deactivating staff
- Assigning departments
- Managing staff access through roles

---

## 🔐 Authentication & Authorization

The application uses **Laravel Sanctum** for API authentication.

Staff authentication is handled through a dedicated `staff` guard.

Authenticated staff can be accessed using:

    Auth::guard('staff')->user()

Protected API routes use Sanctum authentication together with staff authorization middleware.

---

## 👥 Staff Roles

The system defines different staff roles according to their responsibilities:

| Role | Responsibility |
|------|----------------|
| General Manager | Overall hotel management and access to system-wide operations |
| Supervisor | Supervises staff and operations within the assigned department |
| Service Manager | Manages service-related operations within the department |
| Employee | Performs assigned operational tasks |

Access to protected functionality depends on the authenticated staff member's role and department.

---

## 🏢 Department-Based Access

Staff members are associated with departments.

Department-based authorization is used to control access to functionality such as fixed task templates.

For example:

- **General Manager** can access all fixed task templates.
- **Supervisor** can access templates related to their department.
- **Service Manager** can access templates related to their department.
- Other roles are restricted from accessing fixed task management.

---

## 📋 Task Management

The system includes task management for hotel staff.

Tasks can be associated with:

- Staff members
- Fixed task templates
- Task items
- Service operations

The system also considers staff availability and existing workload when assigning operational work.

A staff member does not simply become unavailable because their shift has ended.

If the staff member still has pending or in-progress work, their assigned tasks remain accessible until the work is completed.

At the same time, assigning new work is restricted according to the staff member's current availability and shift rules.

---

## 🧩 Fixed Tasks

The system supports predefined task templates through fixed tasks.

Fixed tasks provide reusable definitions for recurring hotel operations.

Access is controlled according to staff role and department.

Endpoint:

    GET /api/fixed-tasks

Access is protected using:

    auth:sanctum
    staff

---

## 🧹 Guest Service Requests

Guests can request hotel services through the system.

Service requests are connected to active bookings and are handled through the staff workflow.

A service request cannot be created unless the customer has an active booking.

The system uses the configured hotel timezone:

    Asia/Damascus

---

## 🏗️ Backend Architecture

The backend follows a layered architecture designed to keep controllers lightweight and business logic organized.

    Request
       |
      Route
       |
    Middleware
       |
    Controller
       |
    Form Request
       |
    Service Layer
       |
    Eloquent Model
       |
    MySQL Database

### Controllers

Controllers are responsible for handling HTTP requests and returning API responses.

### Form Requests

Form Requests handle:

- Input validation
- Required fields
- Data formats
- Business-related validation rules

### Services

Service classes contain the main business logic and keep controllers focused on request handling.

### Models

Eloquent models represent database entities and their relationships.

---

## 📁 Project Structure

    app/
    ├── Http/
    │   ├── Controllers/
    │   ├── Requests/
    │   └── Resources/
    │
    ├── Models/
    │
    └── Services/

    database/
    ├── migrations/
    └── seeders/

    routes/
    └── api.php

    config/
    bootstrap/
    public/
    resources/
    storage/
    tests/

---

## 🗄️ Database

The project uses **MySQL** with the database:

    hotel_management

The system contains entities for the main hotel operations, including:

    Customers
    Staff
    Departments
    Rooms
    Bookings
    Tasks
    Fixed Tasks
    Task Items
    Service Requests

Relationships between these entities are handled through Laravel Eloquent relationships and database foreign keys.

---

## 🔌 REST API

The application exposes RESTful API endpoints for the different areas of the system.

### Authentication

    POST   /api/login
    POST   /api/logout
    GET    /api/user

### Customers

Customer-related endpoints handle customer information and booking-related operations.

### Rooms

    GET      /api/rooms
    POST     /api/rooms
    GET      /api/rooms/{id}
    PUT      /api/rooms/{id}
    PATCH    /api/rooms/{id}
    DELETE   /api/rooms/{id}

Room modification operations are protected according to the application's authorization rules.

### Staff

    POST   /api/staff

Staff management also includes operations for updating roles and active status.

### Fixed Tasks

    GET   /api/fixed-tasks

Access depends on the authenticated staff member's role and department.

### Bookings & Service Requests

The API provides protected endpoints for booking operations and guest service requests.

Service request operations require an active booking.

---

## 🔒 Security

The backend applies several layers of protection:

- Laravel Sanctum authentication
- Dedicated staff authentication guard
- Role-based authorization
- Department-based access control
- Form Request validation
- Protected API routes
- User/staff ownership checks
- Database relationships and foreign keys
- Validation before performing dependent operations

---

## 🚀 Installation

### Requirements

Make sure the following are installed:

- PHP
- Composer
- MySQL
- Laravel
- Node.js & npm
- Git

### 1. Clone the Repository

    git clone https://github.com/esraaghneem/hotel-management.git

Move into the project directory:

    cd hotel-management

### 2. Install PHP Dependencies

    composer install

### 3. Configure Environment

Create the `.env` file:

    copy .env.example .env

Generate the application key:

    php artisan key:generate

Configure the database connection in `.env`:

    DB_DATABASE=hotel_management
    DB_USERNAME=your_username
    DB_PASSWORD=your_password

### 4. Run Migrations

    php artisan migrate

### 5. Create Storage Link

    php artisan storage:link

### 6. Start the Server

    php artisan serve

The API will be available at:

    http://127.0.0.1:8000

---

## 🧪 API Testing

The API was tested using **Postman**.

Protected endpoints require a Sanctum Bearer Token.

    Authorization: Bearer YOUR_TOKEN

A typical authentication flow is:

    Login
      |
    Receive Sanctum Token
      |
    Send Token with Protected Requests
      |
    Middleware Validates Authentication
      |
    Role / Department Authorization
      |
    Controller
      |
    Service
      |
    Database

---

## 🌐 Deployment

The backend is deployed using **Railway**.

Live deployment:

    https://hotel-management-system-production-97bb.up.railway.app

The project source code is available on GitHub:

    https://github.com/esraaghneem/hotel-management

---

## 🧠 Key Backend Concepts Demonstrated

This project demonstrates practical backend development concepts including:

- REST API design
- Laravel MVC
- Service Layer architecture
- Eloquent relationships
- Form Request validation
- API Resources
- Authentication with Laravel Sanctum
- Role-Based Access Control
- Department-based authorization
- Custom authentication guards
- Database relationships
- Business rule validation
- Staff workload handling
- Booking-dependent service requests
- File/image handling
- Protected API routes
- API testing with Postman
- Git/GitHub workflow
- Laravel deployment with Railway

---

## 📌 Project Goals

The project was developed to simulate real hotel operations while applying backend engineering principles such as:

- Separation of concerns
- Maintainable business logic
- Secure authentication
- Authorization
- Data validation
- Reusable services
- Scalable API structure
- Real-world business rules

---

## 👩‍💻 Author

**Esraa Ghneem**

Backend Developer

GitHub:

https://github.com/esraaghneem

---

## 📄 License

This project was developed for educational and portfolio purposes.
