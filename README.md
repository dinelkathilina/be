## Description

User Management System API built with [NestJS](https://github.com/nestjs/nest), TypeORM, and PostgreSQL.
Features include User Registration, Login (JWT), and Role-Based Access Control (RBAC).

## Prerequisites

- [Node.js](https://nodejs.org/) (v16 or higher)
- [PostgreSQL](https://www.postgresql.org/) (installed and running)

## Installation

1.  Clone the repository:

    ```bash
    git clone https://github.com/dinelkathilina/be.git
    cd be
    ```

2.  Install dependencies:
    ```bash
    npm install
    ```

## Configuration

1.  Create a `.env` file in the root directory by copying the example file:

    ```bash
    cp .env.example .env
    ```

2.  Update the `.env` file with your PostgreSQL credentials:
    ```env
    DB_HOST=localhost
    DB_PORT=5432
    DB_USERNAME=postgres  <-- Replace with your DB username
    DB_PASSWORD=postgres  <-- Replace with your DB password
    DB_NAME=ums_db
    JWT_SECRET=your_jwt_secret_key
    ```

## Database Setup

1.  Ensure PostgreSQL is running.
2.  You can use the provided helper script to create the database (if it doesn't exist) using the credentials from `.env` (or default):
    ```bash
    node create-db.js
    ```
    _Note: This script blindly attempts to create the DB. You might need to adjust it or create the DB manually via pgAdmin or psql._

## Running the app

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```

## API Endpoints & Frontend Integration

The backend runs on `http://localhost:5000` by default.

### 1. Authentication

**Register**

- **URL**: `/auth/register`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "strongpassword",
    "role": "user"
  }
  ```
  _Note: `role` can be "user" or "admin"._

**Login**

- **URL**: `/auth/login`
- **Method**: `POST`
- **Body**:
  ```json
  {
    "email": "john@example.com",
    "password": "strongpassword"
  }
  ```
- **Response**:
  ```json
  {
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI..."
  }
  ```

### 2. Accessing Protected Routes

All protected routes require the `Authorization` header with the Bearer token received from login.

**Header Format**:

```
Authorization: Bearer <your_access_token>
```

**Get User Profile**

- **URL**: `/users`
- **Method**: `GET`
- **Headers**: Requires Bearer Token
- **Response**: Returns the logged-in user's details.

**Get Admin Data**

- **URL**: `/users/admin`
- **Method**: `GET`
- **Headers**: Requires Bearer Token (User must have `role: admin`)
- **Response**: Returns admin-specific data.

## Verification script

You can run the included verification script to test the auth flow:

```bash
node test-auth.js
```

## Support

Nest is an MIT-licensed open source project. It can grow thanks to the sponsors and support by the amazing backers. If you'd like to join them, please [read more here](https://docs.nestjs.com/support).

## License

Nest is [MIT licensed](https://github.com/nestjs/nest/blob/master/LICENSE).
