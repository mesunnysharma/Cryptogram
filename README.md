# Cryptogram 🔐

A real-time chat application where messages are stored encrypted. Built with the MERN stack and Socket.io, using a hybrid scheme: each message is encrypted with AES-256, and the AES key is wrapped with RSA.

## Features

- Sign up and log in with JWT authentication (httpOnly cookies) and bcrypt password hashing
- Real-time one-to-one messaging with Socket.io, including online status
- Messages encrypted with AES-256-CBC; AES keys protected with RSA key pairs
- Conversation list and message history stored in MongoDB
- Responsive UI built with React, Tailwind CSS and DaisyUI, with toast notifications and loading skeletons

## Tech stack

| Layer | Tech |
|---|---|
| Frontend | React 18, Vite, Zustand, React Router, Tailwind CSS, DaisyUI, socket.io-client |
| Backend | Node.js, Express, Socket.io, Mongoose |
| Database | MongoDB |
| Security | JWT, bcryptjs, Node `crypto` (AES-256, RSA) |

## Project structure

```
backend/
  controllers/   request handlers
  cryptservice/  AES and RSA helpers
  models/        user, conversation, message and key models
  routes/        auth, user, message and decryption routes
  socket/        Socket.io server
frontend/
  src/           React app (components, hooks, contexts, zustand store)
```

## Getting started

1. Clone the repo and install dependencies
   ```bash
   npm install
   npm install --prefix frontend
   ```
2. Create a `.env` file in the project root
   ```
   PORT=5000
   MONGO_DB_URI=<your MongoDB connection string>
   JWT_SECRET=<a long random string>
   ```
3. Start the backend and the frontend (in two terminals)
   ```bash
   npm run server
   npm run dev --prefix frontend
   ```

## How the encryption works

1. When a message is sent, a random 256-bit AES key encrypts the text (AES-256-CBC).
2. The AES key is encrypted with an RSA public key.
3. The encrypted message and encrypted key are stored in MongoDB, so the database never holds plain text.
4. On the receiving side the AES key is decrypted with the RSA private key, then the message is decrypted.

## Author

Sunny Kumar · [LinkedIn](https://www.linkedin.com/in/sunny-kumar-517657229) · [GitHub](https://github.com/mesunnysharma)
