# 🏆 ft_transcendence: Real-time Online Pong Game Platform

![Language: TypeScript](https://img.shields.io/badge/Language-TypeScript-blue.svg)
![Frontend: React.js](https://img.shields.io/badge/Frontend-React.js-blue.svg)
![Backend: NestJS](https://img.shields.io/badge/Backend-NestJS-red.svg)
![Database: PostgreSQL](https://img.shields.io/badge/Database-PostgreSQL-blue.svg)
![Orchestration: Docker_Compose](https://img.shields.io/badge/Orchestration-Docker_Compose-green.svg)
![School: 42 Paris](https://img.shields.io/badge/School-42_Paris-orange.svg)
![Grade: 100/100](https://img.shields.io/badge/Grade-100/100-brightgreen.svg)
![Team Project](https://img.shields.io/badge/Team_Project-Yes-blue.svg)

## ✨ Overview

`ft_transcendence` is the demanding final core project from 42 Paris, focused on building a **real-time online multiplayer Pong game platform**. This fullstack web application aims to provide a comprehensive user experience, including user accounts, a chat system, and dynamic multiplayer gameplay, all delivered through a responsive Single-Page Application (SPA).

As a **team project**, it required integrating various modern web technologies, managing complex real-time interactions, and adhering to strict security and design specifications. This endeavor showcased collaborative development skills and the ability to deliver a robust, production-ready web platform.

## 🌟 Key Features & Implementation Details (Mandatory Part)

This project implements a complete online gaming platform with the following core functionalities:

### **1. User Account & Authentication**

*   **42 Intranet OAuth Login:** Users authenticate securely via the 42 intranet's OAuth system.
*   **Unique Profile:** Allows users to choose unique display names and upload custom avatars (with default fallback).
*   **User Profiles:** Displays user statistics (wins, losses, ladder level, achievements) and a comprehensive Match History for 1v1 and ladder games.
*   **Friend System:** Ability to add other users as friends and view their real-time online/in-game status.
*   **Two-Factor Authentication (2FA):** Support for 2FA as a security measure, including **email-based verification or Google Authenticator** (if implemented).
*   **Security Concerns:** Implemented password hashing (e.g., Argon2, bcrypt), protection against SQL injections, and server-side validation for all user input. Authentication managed using **JSON Web Tokens (JWT)**. All credentials are managed via `.env` files and not committed to the repository.

### **2. Real-time Chat System**

*   **Direct & Channel Messaging:** Users can send private messages to friends and participate in public or password-protected chat channels.
*   **Channel Management:** Includes creating, joining, leaving channels, setting/changing topics, and managing channel ownership.
*   **Moderation (Operators):** Channel owners and administrators can manage users (kick, ban, mute) and modify channel modes (invite-only, key, operator privileges, user limit).
*   **User Blocking:** Allows users to block others, preventing messages from blocked accounts.
*   **In-Game Integration:** Facilitates inviting other users to a Pong game directly through the chat interface.

### **3. Online Multiplayer Pong Game**

*   **Live Gameplay:** Users can play a real-time, live Pong game against another player directly on the website.
*   **Matchmaking System:** Integrates a queue-based matchmaking system to automatically pair players.
*   **Responsive Gameplay:** Designed for a responsive and smooth user experience, actively managing potential network issues (lag, disconnections).
*   **Game Customization:** Provides options for game customization (e.g., power-ups, different maps), while also offering a default game version.
*   **Core Game Logic:** Faithful implementation of the original Pong (1972) rules and physics.

### **4. Fullstack Architecture & Deployment**

*   **Frontend (SPA):** Developed as a Single-Page Application (SPA) using **React.js (TypeScript)** for a dynamic and interactive user interface. Supports browser history navigation (back/forward buttons).
*   **Backend (API):** Implemented a robust backend using **NestJS** to manage all game logic, user data, authentication, and chat functionalities.
*   **Database:** Utilizes a **PostgreSQL** database (version 15) for persistent storage of user profiles, game data, chat history, and other application data, with **health checks** for reliable startup.
*   **Containerization:** The entire application stack (frontend, backend, database) is deployed using **Docker containers**, orchestrated with **Docker Compose** for easy setup and management. All Docker images are custom-built.
*   **Persistent Storage:** Uses Docker volumes to ensure persistence of static assets and other dynamic data (e.g., user avatars).

## 🛠️ Technologies Used

*   **Frontend:** React.js, TypeScript
*   **Backend:** NestJS, Node.js, Express.js (NestJS builds on Express)
*   **Database:** PostgreSQL (v15)
*   **Real-time Communication:** WebSockets (via NestJS)
*   **Containerization:** Docker, Docker Compose
*   **Protocols:** RESTful APIs, OAuth 2.0 (for 42 intranet authentication), JSON Web Tokens (JWT)
*   **Concepts:** Single-Page Application (SPA), User Authentication, Game Logic, Chat Systems, Matchmaking, Data Persistence, Inter-service Communication (Docker Networking), Health Checks, Email Integration (for 2FA/notifications).

## 🚀 How to Set Up & Run

To get the `ft_transcendence` platform up and running:

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/ft_transcendence.git
    cd ft_transcendence
    ```
2.  **Configure Environment Variables:**
    A `.env` file is required in the root of the repository. Populate it with the necessary credentials and configuration details for the database, 42 API, JWT, and email service.
    *   **Example `.env` structure (based on `docker-compose.yml`):**
        ```dotenv
        # Database Configuration
        DB_USER=your_db_user
        DB_PW=your_db_password
        DB_NAME=transcendence_db
        DB_PORT=5432
        DB_URL=postgresql://${DB_USER}:${DB_PW}@postgres:${DB_PORT}/${DB_NAME}

        # 42 API OAuth
        FORTYTWO_API_ID=your_42_client_id
        FORTYTWO_API_SECRET=your_42_client_secret
        FORTYTWO_API_CALLBACK=http://localhost:3000/auth/callback # Adjust if frontend port changes

        # JWT Secret
        JWT_SECRET=a_very_long_and_complex_jwt_secret_key

        # Mailer Configuration (for 2FA, if implemented)
        MAILERHOST_USER=your_email_user
        MAILERHOST_PW=your_email_password

        # Docker Virtual Hosts & Ports
        FRONT_URL=http://localhost:3000
        FRONT_VIRTUAL_HOST=localhost
        FRONT_VIRTUAL_PORT=3000

        BACK_URL=http://localhost:3001 # Or whatever your backend directly exposes
        BACK_VIRTUAL_HOST=localhost
        BACK_VIRTUAL_PORT=3001
        NETWORK_NAME=transcendence_network
        ```
    *   *Note: Adjust `FRONT_VIRTUAL_HOST` / `FRONT_VIRTUAL_PORT` and `BACK_VIRTUAL_HOST` / `BACK_VIRTUAL_PORT` in your `.env` to match your local setup for frontend and backend access.*

3.  **Launch the Infrastructure:**
    ```bash
    docker compose up --build
    ```
    This command will build all necessary Docker images, start the containers (frontend, backend, database), and connect them within the Docker network.
    *Ensure Docker and Docker Compose are installed and running on your system.*

4.  **Access the Application:**
    Once the services are up (this might take a few moments), you can access the application via your web browser at the `FRONT_URL` you configured (e.g., `http://localhost:3000`).

## 🎓 Learning Outcomes

This project provided invaluable experience in:

*   **Fullstack Web Development:** Building and integrating complex frontend (React.js), backend (NestJS), and database (PostgreSQL) components.
*   **Real-time Application Development:** Implementing chat and game logic using real-time communication protocols (e.g., WebSockets).
*   **Containerization & Orchestration:** Proficiently using Docker and Docker Compose for multi-service application deployment with health checks.
*   **Database Design & Integration:** Designing relational schemas, interacting with PostgreSQL, and ensuring database readiness.
*   **Authentication & Security:** Implementing OAuth (42 API), JSON Web Tokens (JWT), password hashing, server-side validation, and **Two-Factor Authentication (2FA) with email integration**.
*   **Game Development:** Designing game logic, matchmaking systems, and responsive user interfaces.
*   **Collaborative Development:** Effectively working in a team on a large and complex codebase, managing version control and code integration.
*   **Single-Page Application (SPA) Development:** Understanding SPA principles and browser history management.


Made by:
[https://github.com/NeronTheTyrant](Martin Lebard)
[https://github.com/mchibane](Mehdi Chibane)
[https://github.com/TsakBoolhak](Aurélien Cabiac)
[https://github.com/LeoBourret](Léo Bourret)

