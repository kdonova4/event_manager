# Mini Project: Event Management System

## Requirements
### Spring Boot Basics

- Use dependency injection for beans.
- Apply Spring Boot annotations to configure and manage the application.

### Spring MVC

- Implement the 3-layer architecture: Controllers, Services, and Repositories.
- Separate logic into appropriate layers for maintainability.

### Database Integration

- Use MySQL for persistence.
- Design a normalized database schema in 3NF.
- Perform advanced queries using Spring Data JPA.

### RESTful APIs

- Design RESTful APIs for event and user management.
- Document APIs using Swagger/OpenAPI.

### Authentication

- Implement JWT for authentication.
- Apply role-based access control (RBAC) to restrict API access based on user roles.

## Functional Requirements
#### User Management

- Organizer can:
    - Register and log in.
    - Manage their profile.
- Attendee can:
    - Register and log in.
    - View and manage their profile.

#### Event Management

- Organizer can:
    - Create, update, and delete events.
    - View all events they have created.
    - View a list of attendees for each event.
- Attendee can:
    - Browse available events.
    - Register for events.
    - Cancel their registration for events.
    - View all events they are registered for.

### Authentication and Authorization

- Use JWT tokens for authentication.
- Enforce RBAC:
    - Organizers can only access /organizer/** endpoints.
    - Attendees can only access /attendee/** endpoints.

# Step-by-Step Instructions
## 1. Setup

- Create a new Spring Boot project with the following dependencies:
    - Spring Web
    - Spring Data JPA
    - Spring Security
    - MySQL Driver
    - Lombok
    - Swagger/OpenAPI
- Configure application.properties for:
    - MySQL database connection.
    - JWT secret key and expiration time.

## 2. Database Design

### Design the following tables:

- Users
    - id (Primary Key)
    - username (Unique)
    - password
    - email
    - role (ENUM: ORGANIZER, ATTENDEE)
- Events
    - id (Primary Key)
    - title
    - description
    - date (DATE)
    - location
    - organizer_id (Foreign Key referencing Users.id)
- EventRegistrations
    - id (Primary Key)
    - event_id (Foreign Key referencing Events.id)
    - attendee_id (Foreign Key referencing Users.id)

## 3. Backend Development
### Authentication

- Create a utility class for token generation and validation.
- Implement a filter to validate JWT tokens for each request.
- Add login and registration endpoints.

### RBAC Implementation

- Use Spring Security to define roles (ORGANIZER, ATTENDEE).
- Restrict access using annotations:
    - @PreAuthorize("hasRole('ORGANIZER')")
    - @PreAuthorize("hasRole('ATTENDEE')")

### API Endpoints

- User Controller
    - POST /register: Register a new user.
    - POST /login: Authenticate a user and return a JWT.
    - GET /profile: Get the logged-in user's profile.
    - PUT /profile: Update the logged-in user's profile.
- Organizer Controller
    - POST /organizer/events: Create a new event.
    - GET /organizer/events: List all events created by the organizer.
    - PUT /organizer/events/{id}: Update an event.
    - DELETE /organizer/events/{id}: Delete an event.
    - GET /organizer/events/{id}/attendees: List attendees for a specific event.
- Attendee Controller
    - GET /attendee/events: Browse available events.
    - POST /attendee/events/{id}/register: Register for an event.
    - DELETE /attendee/events/{id}/register: Cancel registration.
    - GET /attendee/events: View all registered events.

### Service Layer

- Implement business logic for users and events.
- Add validation to ensure only valid operations are performed (e.g., an organizer can only modify their own events).

### Repository Layer

- Use Spring Data JPA for CRUD operations.
- Add custom methods for querying attendees for an event and events for a user.

## 4. Testing
### Unit Tests

- Write unit tests for service methods using JUnit and Mockito.
- Mock dependencies to isolate tests.

### Integration Tests

- manually test all API endpoints.
- Verify JWT authentication and role-based access control.

### Deliverables

- Fully functional application with a GitHub repository.
- MySQL script to set up the database schema.
- Swagger/OpenAPI documentation for all endpoints.
- A README file detailing:
    - Project overview.
    - Setup instructions.
    - API usage examples.
    - Unit and integration test results.

### Bonus Stretch Goals

- Implement event search functionality (e.g., search by date, location).
- Add email notifications for event registrations.
- Use pagination and sorting for event lists.
- Allow attendees to leave feedback for events they attended.

### Self-Evaluation Criteria

- Completeness: Does the project meet the stated requirements?
- Code Quality: Is the code modular, readable, and well-structured?
- Security: Are JWT and RBAC implemented correctly?
- Database Design: Is the database schema normalized and efficient?
- Testing: Are unit and integration tests thorough and meaningful?

