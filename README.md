# ChatVerse

![React 19](https://img.shields.io/badge/React-19.1.1-61DAFB?style=flat&logo=react&logoColor=black)
![Vite](https://img.shields.io/badge/Vite-7.1.7-646CFF?style=flat&logo=vite&logoColor=white)
![NodeJS](https://img.shields.io/badge/Node.js-Express_5.2-339933?style=flat&logo=nodedotjs&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-4.8.3-010101?style=flat&logo=socketdotio&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Mongoose_9.7-47A248?style=flat&logo=mongodb&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-v4-06B6D4?style=flat&logo=tailwindcss&logoColor=white)
![Zustand](https://img.shields.io/badge/Zustand-5.0-brown?style=flat)

A full-stack, bi-directional instant messaging and social status application built on the MERN stack with Socket.IO and WebSockets. Designed to deliver low-latency messaging, optimistic UI rendering, live user presence tracking, dynamic typing indicators, read receipts, emoji reactions, and 24-hour disappearing media stories.

---

## Key Highlights

- **Bi-Directional Real-Time Messaging**: Built on Socket.IO 4.8 with point-to-point recipient emits (`io.to(receiverSocketId)`) for sub-50ms message latency and reduced server bandwidth.
- **Live Presence & Heartbeat Tracking**: Real-time tracking of active online/offline status with automatic tab switch and connection lifecycle handling.
- **Intelligent Typing Indicators**: Server-debounced typing streams (3-second auto-clearing timeouts) paired with client throttling to prevent WebSocket event thrashing.
- **Interactive Read Receipts & Message Reactions**: Real-time delivered/read checkmarks and dynamic emoji reaction tray popups.
- **Status Stories**: 24-hour ephemeral image/media stories powered by Multer memory storage and Cloudinary CDN delivery.
- **Modern Responsive UI**: Built with React 19, Vite 7, Tailwind CSS v4, DaisyUI themes, Framer Motion animations, and mobile/desktop responsive drawers.
- **End-to-End Auth Guards**: Secure JWT cookie authentication, protected routes (`protected.jsx`), Yup + React-Hook-Form payload validation, and CORS protection.

---

## Architecture & Tech Stack

### Frontend
- **Framework**: [React 19](https://react.dev/) + [Vite 7](https://vitejs.dev/)
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/) & [DaisyUI 5](https://daisyui.com/)
- **State Management**: [Zustand 5](https://github.com/pmndrs/zustand) (`chatStore.js`, `useUserStore.js`, `useThemeStore.js`, `layoutStore.js`)
- **Animation & Transitions**: [Framer Motion 12](https://www.framer.com/motion/)
- **Routing**: [React Router DOM v7](https://reactrouter.com/)
- **WebSocket Client**: [Socket.io-client 4.8](https://socket.io/)
- **Forms & Validation**: React-Hook-Form + Yup
- **Utilities**: Emoji-Picker-React, React-Icons, Axios, Date-fns, React-Toastify

### Backend
- **Runtime & Server**: [Node.js](https://nodejs.org/) (ES Modules) & [Express.js 5.2](https://expressjs.com/)
- **Real-Time Engine**: [Socket.IO 4.8](https://socket.io/) with custom lifecycle listeners
- **Database & ODM**: [MongoDB](https://www.mongodb.com/) via [Mongoose 9.7](https://mongoosejs.com/)
- **Security & Auth**: JSON Web Tokens (JWT), Cookie-Parser, bcrypt / secure hashing
- **Media Ingestion**: [Cloudinary SDK](https://cloudinary.com/) + [Multer 2](https://github.com/expressjs/multer)
- **Notifications & SMS**: Nodemailer & Twilio integration

---

## Project Structure

```bash
Real-Time-Chat-Application/
├── backend/
│   ├── config/              # Database connection (dbConfig.js)
│   ├── controllers/         # Business logic (Auth, Chat, Status/Story controllers)
│   ├── middleware/          # JWT auth guard & Multer memory storage parsers
│   ├── models/              # Mongoose database schemas:
│   │   ├── conversation.model.js  # Participants, last message snippet, unread counter
│   │   ├── message.model.js       # Content, media URL, sender, receiver, read status, reactions
│   │   ├── status.model.js        # 24-hour expiring media stories
│   │   └── user.model.js          # User profiles, avatar, bio, phone, online state
│   ├── routes/              # Express REST API endpoints (auth, chat, status)
│   ├── services/
│   │   └── socket.service.js# Socket.IO connection handling, typing state, reactions
│   ├── utils/               # Cloudinary upload helpers, JWT token generators, Twilio/Nodemailer
│   ├── index.js             # HTTP & WebSocket server entry point
│   └── package.json
│
└── frontend/
    ├── src/
    │   ├── components/      # Reusable UI widgets, navigation bars, modals, media previews
    │   ├── hooks/           # Custom React hooks for socket events & screen responsiveness
    │   ├── pages/
    │   │   ├── chatSection/ # ChatList, ChatWindow, MessageBubble, EmojiPicker
    │   │   ├── settingSection/# Profile editor, DaisyUI multi-theme switcher, privacy
    │   │   ├── statusSection/ # Ephemeral 24hr disappearing stories
    │   │   └── user-login/  # Email/Phone login & register with validation
    │   ├── services/        # Centralized Axios API request clients
    │   ├── store/           # Zustand reactive stores (chat, user, theme, layout)
    │   ├── protected.jsx    # Client-side protected route wrapper
    │   ├── App.jsx          # Route declarations & socket lifecycle listeners
    │   └── main.jsx
    ├── package.json
    └── vite.config.js
```

---

## Getting Started

### 1. Prerequisites
- **Node.js** (v18.x or higher)
- **MongoDB** (Local instance or MongoDB Atlas cluster URI)
- **Cloudinary Account** (For image/media storage)

### 2. Environment Variables

Create a `.env` file in the `backend/` directory:

```env
PORT=5000
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/chatapp?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_jwt_key
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# Optional: Notification services
TWILIO_ACCOUNT_SID=your_twilio_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_PHONE_NUMBER=your_twilio_number
EMAIL_USER=your_email@domain.com
EMAIL_PASS=your_email_app_password
```

Create a `.env` file in the `frontend/` directory (if needed):

```env
VITE_API_URL=http://localhost:5000
VITE_SOCKET_URL=http://localhost:5000
```

---

### 3. Installation & Running Locally

#### Start the Backend Server:
```bash
cd backend
npm install
npm run dev
```
> Server runs on `http://localhost:5000` with WebSocket listeners enabled.

#### Start the Frontend Client:
```bash
cd frontend
npm install
npm run dev
```
> Vite development server starts on `http://localhost:5173`.

---

## Real-Time WebSocket Events Matrix

| Event Name | Direction | Payload | Description |
|---|---|---|---|
| `connection` | Client -> Server | `userId` | Registers client socket and maps active user connection |
| `getOnlineUsers` | Server -> Client | `[userId1, userId2]` | Broadcasts updated roster of currently online users |
| `send_message` | Client -> Server | `{ receiverId, text, image }` | Sends message to server for persistence and routing |
| `receive_message`| Server -> Client | `MessageObject` | Delivers real-time message strictly to recipient socket |
| `typing_start` | Client -> Server | `{ receiverId }` | Triggers active typing indicator for conversation partner |
| `typing_stop` | Client -> Server | `{ receiverId }` | Clears typing indicator (auto-debounced to 3 seconds) |
| `add_reaction` | Client -> Server | `{ messageId, emoji }` | Updates message with live emoji reaction |

---

## Security & Performance Best Practices

1. **Point-to-Point Socket Delivery**: Avoided broad `io.emit()` broadcast leaks by scoping user events directly to target client sockets (`io.to(receiverSocketId)`).
2. **Debounced Network Streams**: Eliminated typing event flooding by throttling client emits and enforcing 3s server inactivity timers.
3. **Cookie-Based HTTP-Only JWTs**: Defends against XSS vulnerabilities by keeping authentication tokens out of `localStorage`.
4. **Optimistic Store Updates**: Zustand store updates message feeds immediately before network resolution to deliver instantaneous UI feedback.

---

## License
This project is open-source and available under the [ISC License](LICENSE).
