# Student Registration System with 2-Level Encryption

A full-stack application for student registration and management, featuring a unique dual-layer encryption architecture for sensitive data.

## Tech Stack

- **Frontend**: React, TypeScript, Vite, Tailwind CSS, React Hook Form, Axios, Lucide React
- **Backend**: Node.js, Express, TypeScript
- **Database**: MongoDB (Mongoose)
- **Security**: AES Encryption (CryptoJS), Password Hashing (bcryptjs)

## Encryption Implementation

This project implements a **2-level encryption** strategy as follows:

1.  **Level 1 (Frontend)**: Before sending data to the backend, the client encrypts the student's personal information (excluding email for lookup) using AES with a `FRONTEND_SECRET`.
2.  **Backend Processing**: Upon receiving the encrypted payload, the backend decrypts it using the `FRONTEND_SECRET`.
3.  **Password Security**: The student's password is never stored as plaintext or AES-encrypted. Instead, it is hashed using **bcryptjs** before storage.
4.  **Level 2 (Backend)**: The backend applies a second layer of AES encryption using a `BACKEND_SECRET` to the student's personal data before saving it to MongoDB.
5.  **Data Fetching**:
    - Backend retrieves data from MongoDB.
    - Decrypts the `BACKEND_SECRET` layer.
    - Re-encrypts with `FRONTEND_SECRET` and sends to client.
    - Client performs the final decryption using `FRONTEND_SECRET`.

## Folder Structure

```text
task-react-node-typescript/
┣ client/             # React frontend
┃ ┣ src/
┃ ┃ ┣ components/     # UI Components (LoginForm, StudentForm, StudentList)
┃ ┃ ┣ pages/          # Page Containers (Dashboard)
┃ ┃ ┣ services/       # API calling logic
┃ ┃ ┣ utils/          # Crypto utilities (Frontend secret)
┃ ┃ ┗ types/          # TypeScript definitions
┣ server/             # Node.js backend
┃ ┣ src/
┃ ┃ ┣ controllers/    # Request handlers (Student CRUD + Encryption)
┃ ┃ ┣ models/         # Mongoose schemas
┃ ┃ ┣ routes/         # API endpoints
┃ ┃ ┣ config/         # Database connection
┃ ┃ ┗ utils/          # Crypto utilities (Backend secret)
┗ README.md
```

## Setup Instructions

### Prerequisites
- Node.js (v16+)
- MongoDB (running locally or on Atlas)

### Backend Setup
1. Navigate to the server folder: `cd server`
2. Install dependencies: `npm install`
3. Configure `.env` file (sample provided):
   ```env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/student_db
   FRONTEND_SECRET=your_frontend_secret
   BACKEND_SECRET=your_backend_secret
   ```
4. Start development server: `npm run dev`

### Frontend Setup
1. Navigate to the client folder: `cd client`
2. Install dependencies: `npm install`
3. Configure `.env` file:
   ```env
   VITE_API_URL=http://localhost:5000/api
   VITE_FRONTEND_SECRET=your_frontend_secret
   ```
4. Start development server: `npm run dev`

## Features
- ✨ **Premium UI**: Modern dark theme with glassmorphism and smooth animations.
- 🔐 **Dual-Layer Security**: AES encryption at both frontend and backend layers.
- 📝 **Full CRUD**: Register, view, update, and delete students.
- ✅ **Validation**: Comprehensive form validation using React Hook Form.
- 📱 **Responsive**: Fully responsive design for all screen sizes.
