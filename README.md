# Chat App

This is a full-stack, real-time chat application built with a React frontend and a Node.js backend. It leverages WebSockets for instant messaging and features user authentication, including Google OAuth.

## 🚀 Features

-   **Real-Time Messaging:** Instant message delivery using WebSockets.
-   **User Authentication:** Secure user registration and login with password hashing (Argon2).
-   **Google OAuth 2.0:** Sign in easily and securely with your Google account.
-   **Online User List:** See who is currently active in the chat.
-   **Message History:** Loads the last 30 messages upon joining the chat.
-   **Avatar Uploads:** Users can upload a profile picture during registration.
-   **Protected Routes:** Chat is only accessible to authenticated users.
-   **Modern UI:** A clean and responsive user interface built with Material-UI.

## 💻 Tech Stack

| Area      | Technologies                                                                                                 |
| :-------- | :----------------------------------------------------------------------------------------------------------- |
| **Frontend**  | React, TypeScript, Redux Toolkit, Vite, React Router, Axios, Material-UI, `react-oauth/google`, WebSockets |
| **Backend**   | Node.js, Express, TypeScript, MongoDB (Mongoose), `express-ws` (WebSockets), JSON Web Tokens (JWT), Argon2   |

## 🛠️  Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

-   [Node.js](https://nodejs.org/) (v20.19.0 or later)
-   [npm](https://www.npmjs.com/)
-   [MongoDB](https://www.mongodb.com/) (Make sure your MongoDB server is running)

### Backend Setup

1.  **Navigate to the backend directory:**
    ```sh
    cd backend
    ```

2.  **Install dependencies:**
    ```sh
    npm install
    ```

3.  **Set up environment variables:**
    Create a `.env` file in the `backend` directory by copying the template:
    ```sh
    cp .env.template .env
    ```
    Open the `.env` file and fill in your details:
    ```
    JWT_SECRET=your_jwt_secret_key
    CLIENT_ID=your_google_client_id
    CLIENT_SECRET=your_google_client_secret
    ```

4.  **Start the backend server:**
    ```sh
    npm run dev
    ```
    The server will be running on `http://localhost:8008`.

### Frontend Setup

1.  **Navigate to the frontend directory:**
    ```sh
    cd frontend
    ```

2.  **Install dependencies:**
    ```sh
    npm install
    ```

3.  **Configure Google Client ID:**
    The Google Client ID is hardcoded in `frontend/src/constants.ts`. If you are using your own Google OAuth credentials, update it there.

4.  **Start the frontend development server:**
    ```sh
    npm run dev
    ```
    The application will be available at `http://localhost:5173`.

## ▶️ WebSocket Communication

The client and server communicate over WebSockets using a simple JSON-based protocol.

### Incoming Messages (Client to Server)

-   `type: 'SEND_MESSAGE'`: Sent when a user sends a new message.
    -   `payload`: A string containing the message text.

### Outgoing Messages (Server to Client)

-   `type: 'HISTORY'`: Sent to a client upon connection, containing a history of the last 30 messages.
    -   `payload`: An array of `ChatMessage` objects.
-   `type: 'NEW_MESSAGE'`: Broadcast to all connected clients when a new message is sent.
    -   `payload`: A single `ChatMessage` object for the new message.
-   `type: 'UPDATE_USER_LIST'`: Broadcast to all clients when a user connects or disconnects.
    -   `payload`: An array of online `User` objects.
