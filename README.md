# YourPlaces - MERN Full-Stack Places App

## Overview

This workspace contains a full-stack MERN application for managing user-created places. Users can sign up or log in, upload images, create places with addresses, view places by user, and update or delete their own entries. The project is structured as a client/server application with a React frontend and an Express + MongoDB backend.

The application is a practical example of building a modern web app with:
- a decoupled frontend and backend,
- authentication and protected routes,
- file uploads,
- form validation,
- REST-style API design,
- and database-backed CRUD operations.

---

## What This Project Demonstrates

This repository is a strong example of how to build a complete web application using the MERN stack with a clean separation of concerns:

- Frontend handles UI, routing, state, validation, and user experience.
- Backend handles API logic, authentication, database interaction, and file handling.
- MongoDB stores users, places, and relationship data.
- The app demonstrates common real-world development techniques such as reusable hooks, context-based auth, middleware, error handling, and transaction-safe writes.

---

## Core Features

- User authentication with JWT
- Sign up and login flows
- Create, update, and delete places
- Upload place images
- View places associated with a specific user
- Protected routes for authenticated actions
- Client-side validation and loading/error UI feedback
- Geocoding-based location lookup using Google Maps API

---

## Tech Stack

| Layer | Technologies |
|---|---|
| Frontend | React, React Router, CSS Modules-style component styles, React Context API |
| Backend | Node.js, Express.js |
| Database | MongoDB with Mongoose |
| Authentication | JSON Web Tokens (JWT), bcryptjs |
| File Uploads | multer |
| Validation | express-validator |
| External API | Google Geocoding API |
| Development Tools | nodemon, react-scripts |

---

## Architecture and Development Approach

### 1. Frontend Architecture

The frontend is built as a single-page application using React.

Key techniques used:
- Component-based UI design
- React Router v5 for navigation and route protection
- Context API for authentication state
- Custom hooks for reusable logic:
  - form handling
  - HTTP requests
  - auth persistence
- Lazy loading with React.lazy for better loading performance
- Reusable UI components for modals, cards, buttons, inputs, and image upload

The app uses a custom form system instead of relying on a heavy form library. This keeps the code simple and demonstrates how form state and validation can be managed manually in React.

### 2. Backend Architecture

The backend is built with Express and follows a route-controller-model style.

Key techniques used:
- RESTful route organization under separate route files
- Middleware for authentication, file uploads, and validation
- Controllers for business logic
- Mongoose schemas and models for structured MongoDB documents
- Custom error handling using a centralized HttpError model
- Transactions for related write operations such as creating/deleting places

### 3. Authentication Flow

Authentication is handled through JWTs:
- A user signs in or signs up.
- The backend returns a token.
- The frontend stores the token and user info in localStorage.
- Protected routes require a valid token.
- The backend verifies the token using middleware before allowing access to protected endpoints.

### 4. File Upload Handling

The app supports image uploads for users and places using multer. Uploaded files are stored in the server’s uploads directory and served via Express static middleware.

### 5. Geolocation Support

When a user creates a place, the application uses Google Geocoding API to convert the submitted address into latitude and longitude coordinates. These coordinates are stored alongside the place and can later be used for map visualization.

---

## Folder Structure

```text
Mern-Project/
├── BackEnd/
│   ├── app.js
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── uploads/
│   └── util/
├── FrontEnd/
│   ├── public/
│   └── src/
│       ├── App.js
│       ├── places/
│       ├── shared/
│       └── user/
```

### Backend responsibilities
- controllers: request handlers for places and users
- middleware: auth and upload logic
- models: MongoDB schemas
- routes: API endpoint definitions
- util: helper functions such as geocoding

### Frontend responsibilities
- places: place-related pages and components
- user: authentication and user pages
- shared: reusable UI, hooks, context, and utilities

---

## API Overview

The backend exposes REST-style endpoints such as:

### Places
- GET /api/places/:pid - Get a place by id
- GET /api/places/user/:uid - Get places by user
- POST /api/places - Create a place
- PATCH /api/places/:pid - Update a place
- DELETE /api/places/:pid - Delete a place

### Users
- GET /api/users - Fetch users
- POST /api/users/signup - Register a user
- POST /api/users/login - Log in a user

---

## Setup Instructions

### 1. Install dependencies

Open two terminals and run:

```bash
cd BackEnd
npm install
```

```bash
cd FrontEnd
npm install
```

### 2. Configure environment variables

Create a `.env` file inside the backend folder with values similar to:

```env
DB_USER=your_mongodb_username
DB_PASSWORD=your_mongodb_password
DB_NAME=your_database_name
GOOGLE_API_KEY=your_google_geocoding_api_key
JWT_KEY=your_secret_key
```

Create a `.env` file inside the frontend folder if needed:

```env
REACT_APP_BACKEND_URL=http://localhost:5000
```

### 3. Start the backend

```bash
cd BackEnd
npm start
```

This starts the Express server with nodemon on port 5000.

### 4. Start the frontend

```bash
cd FrontEnd
npm start
```

The React app will start in the browser and communicate with the backend API.

---

## Running the Application

Once both servers are running:
- the frontend will be available in the browser,
- authentication and place management operations will be served by the backend,
- and MongoDB will persist the application data.

---

## Key Implementation Techniques

### Reusable custom hooks
The frontend uses custom hooks to make the app cleaner and more modular:
- useForm for managing form validity and input state
- useHttpClient for request lifecycle, loading state, and error handling
- useAuth for persistent login state and token expiration

### Context-based authentication
Auth state is shared globally through React context so pages and components can access login status and user info without prop drilling.

### Middleware-driven backend
The backend relies heavily on middleware for concerns such as:
- request validation,
- authentication,
- file handling,
- CORS support,
- and centralized error responses.

### Controlled form experience
The UI validates form input before submission and shows loading/error states using reusable components.

---

## Notes and Possible Improvements

This project is a solid learning-focused full-stack application, but there are areas that could be improved for production:
- add environment-based production configuration,
- improve image storage strategy using cloud storage,
- add refresh token support,
- separate business logic into services,
- add unit and integration tests,
- improve input validation and user feedback,
- tighten security for production deployment.

---

## Summary

This workspace is a practical MERN application that demonstrates how to connect a React frontend to a Node/Express backend backed by MongoDB. It covers the essentials of full-stack development: routing, authentication, CRUD, validation, uploads, and API design.

If you want, this README can also be expanded with a screenshot section, contribution guidelines, or deployment instructions for Vercel/Render/Heroku.
