# Chirpy - Social Network Backend

Chirpy is a lightweight social network similar to Twitter, developed to experiment with Go and test various backend functionalities. It features basic user authentication, JWT-based authorization, and stores data in the filesystem as a simple database. This document outlines the project's structure, environment setup, and available API endpoints.
 
## Features

User Authentication: Passwords are hashed using bcrypt, and the app supports login, registration, and user updates.

JWT Authorization: Uses access and refresh tokens for managing sessions.

File-based Database: JSON is used to store data persistently in the filesystem.

Chirps: Users can create, retrieve, and delete chirps (equivalent to tweets).

Webhook Integration: Handles webhooks with an API key for external services.

Metrics Page: Exposes a simple admin page for server metrics.

### Environment Variables

Chirpy uses two environment variables, which can be found in the .env.template file. To get started, you should create a .env file in the root directory of your project, using the template as a guide.

    JWT_SECRET: Secret key used for signing JWT tokens.
    POLKA_KEY: API key for webhook authorization.

Ensure these are properly configured before running the application.
Run Flags

Chirpy includes a flag that can be used when starting the server:

    --debug: Deletes and regenerates the JSON database in the filesystem. This is useful for resetting the database during development.

### API Endpoints

Here is a list of the main API endpoints available in Chirpy:
Health Check & Reset

    GET /api/healthz: Check if the server is up and running.
    GET /api/reset: Resets the Metrics.

User Management

    POST /api/users: Create a new user.
    PUT /api/users: Update existing user details.

Authentication

    POST /api/revoke: Revoke a refresh token.
    POST /api/refresh: Obtain a new access token using a refresh token.
    POST /api/login: Authenticate a user and return access/refresh tokens.

Chirps (Posts)

    POST /api/chirps: Create a new chirp.
    GET /api/chirps: Retrieve all chirps (optional sort "asc/desc" query param).
    GET /api/chirps/{chirpID}: Retrieve a specific chirp by ID.
    DELETE /api/chirps/{chirpID}: Delete a specific chirp by ID.

Webhook

    POST /api/polka/webhooks: Receive and handle incoming webhook events (requires an API key).

Admin & Metrics

    GET /admin/metrics: View server metrics on the admin page.

## Setup and Running the Project

To get started with Chirpy:

1. Clone the repository and navigate into the project directory.

2. Install dependencies and create your .env file using .env.template as a guide.

    ```bash
    go mod tidy
    ```

3. Run the application:

    ```bash
    go build -o out && ./out --debug
    ```
