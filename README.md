# DORA - Urdu Voice Scheduler 🎙️📅

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
[![Live Demo](https://img.shields.io/badge/demo-live-orange)](https://dora-urdu-voice-scheduler.vercel.app/)

*An intelligent voice-powered scheduling assistant with natural language understanding in Urdu*

![DORA App](./public/screenshots/ss2-frontend.png)

</div>

## 🌟 Project Overview

**DORA** is an advanced web application that enables users to schedule calendar events using **Urdu voice commands**. Built with modern web technologies, DORA transcribes Urdu speech into text, extracts event details, and automatically schedules them in Google Calendar. The application also features a sophisticated RAG-based chatbot that can answer questions about scheduled events by retrieving relevant information from a vector database.

This project demonstrates the practical application of voice technology, natural language processing, and semantic search to create a seamless, accessible scheduling experience for Urdu-speaking users.

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Live Demo](#-live-demo)
- [Screenshots](#-screenshots)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#️-project-structure)
- [Contributing](#-contributing)
- [Roadmap](#️-roadmap)
- [License](#-license)
- [Acknowledgements](#-acknowledgements)
- [Contributors](#-contributors)

## ✨ Features

### 🎤 Voice Transcription
- Records Urdu voice input through an intuitive interface
- Leverages **OpenAI's Whisper API** for accurate transcription of Urdu speech
- Supports various Urdu dialects and accents

### 📝 Task Extraction
- Analyzes transcribed text using **OpenAI's GPT-4o** model
- Intelligently extracts event details such as title, date, time, location, and participants
- Handles relative time expressions in Urdu (e.g., "کل" for tomorrow, "اگلے ہفتے" for next week)
- Ensures all events are scheduled for future dates

### 🤖 Chatbot Integration
- Implements a **Retrieval-Augmented Generation (RAG)** architecture
- Stores event data as **BERT embeddings** in **Pinecone** vector database
- Enables semantic search for retrieving relevant calendar information
- Answers natural language queries about scheduled events (e.g., "When is my meeting with Abdullah Arif?")
- Provides contextual responses based on the user's calendar data

### 🔐 Authentication
- Secure authentication using **Google OAuth 2.0** via **NextAuth.js**
- Protects user data and calendar access
- Maintains persistent sessions with JWT tokens

### 📅 Calendar Integration
- Seamless integration with **Google Calendar API**
- View, create, edit, and delete calendar events
- Multiple calendar views (day, week, month)
- Real-time synchronization of events

### 🌐 Additional Features
- **Responsive Design**: Optimized for mobile, tablet, and desktop
- **Timezone Management**: Support for various timezones
- **Debug Tools**: Real-time debugging information
- **RTL Support**: Right-to-left layout for Urdu interface

## 🔧 Tech Stack

<div align="center">

| Frontend | Backend | AI & Data | Authentication |
|:--------:|:-------:|:---------:|:-------------:|
| Next.js | Node.js | OpenAI Whisper | NextAuth.js |
| React | API Routes | GPT-4o | Google OAuth |
| Tailwind CSS | TypeScript | Pinecone | JWT |
| Radix UI | date-fns-tz | BERT Embeddings | |

</div>

## 🚀 Live Demo

Experience DORA at: [https://dora-urdu-voice-scheduler.vercel.app/](https://dora-urdu-voice-scheduler.vercel.app/)

## 📸 Screenshots

<div align="center">

### Login Screen
![Login Screen](./public/screenshots/ss1-login.png)

### Calendar View
![Calendar View](./public/screenshots/ss3-calender-view.png)

### Chatbot Interface
![Chatbot Interface](./public/screenshots/ss4-chatbot.png)

### Voice Recording
![Voice Recording](./public/screenshots/ss5-voice-recording.png)

### Event Parsing
![Event Parsing](./public/screenshots/ss6-event-parsing.png)

</div>

## 📋 Installation

### Prerequisites

- **Node.js** (v16+)
- **pnpm** package manager
- **Google Cloud Project** with Calendar API enabled
- **OpenAI API Key** for Whisper transcription and GPT models
- **Pinecone API Key** for vector database

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/abdullaharif381/dora-a3
   cd dora-a3
   ```

2. **Install dependencies**
   ```bash
   pnpm install
   ```

3. **Configure environment variables**

   Create a `.env.local` file in the root directory:
   ```env
   # Authentication
   GOOGLE_CLIENT_ID=your-google-client-id
   GOOGLE_CLIENT_SECRET=your-google-client-secret
   NEXTAUTH_SECRET=your-nextauth-secret
   NEXTAUTH_URL=http://localhost:3000
   
   # OpenAI
   OPENAI_API_KEY=your-openai-api-key
   
   # Pinecone
   PINECONE_API_KEY=your-pinecone-api-key
   ```

4. **Set up Pinecone Index**
   
   Create an index in your Pinecone dashboard with the following configuration:
   - Name: `dorag`
   - Dimensions: `1024`
   - Metric: `cosine`

5. **Start the development server**
   ```bash
   pnpm dev
   ```

6. Access the application at `http://localhost:3000`

## 🔍 Usage

### Voice Scheduling Workflow

1. **Sign in** with your Google account
2. **Record your voice** by clicking the microphone button and speaking your event details in Urdu
3. **Review the extracted event** details that appear after processing
4. **Confirm or edit** the event before adding it to your calendar
5. **View your calendar** to see the newly created event

### Chatbot Interaction

1. Type a question in the chat interface, such as "میری عبداللہ عارف کے ساتھ ملاقات کب ہے؟" (When is my meeting with Abdullah Arif?)
2. The chatbot will:
   - Convert your question into vector embeddings
   - Query the Pinecone database for similar vectors
   - Retrieve relevant event information
   - Generate a contextual response

### Calendar Management

- Switch between **day**, **week**, and **month** views
- Navigate through time periods using the navigation controls
- Click on events to view details or make edits
- Delete events as needed

## 🗂️ Project Structure

```
dora-a3/
├── app/                # Next.js app routes and layouts
├── components/         # React components
│   ├── calendar-view.tsx     # Calendar display component
│   ├── debug-info.tsx        # Debugging information panel
│   ├── timezone-selector.tsx # Timezone selection component
│   ├── voice-recorder.tsx    # Voice recording interface
│   └── ...                   # Other UI components
├── lib/                # Utility functions and services
│   ├── auth.ts               # Authentication configuration
│   ├── calendar-api.ts       # Google Calendar API integration
│   ├── chatWithBot.ts        # RAG chatbot implementation
│   ├── date-utils.ts         # Date formatting utilities
│   ├── extract-event.ts      # Event extraction from transcription
│   └── transcribe.ts         # Voice transcription service
├── public/             # Static assets
└── styles/             # Global styles
```

## 👥 Contributing

Contributions to DORA are welcome! Here's how you can contribute:

1. **Fork** the repository
2. **Create a branch** (`git checkout -b feature/amazing-feature`)
3. **Make changes** following our coding standards
4. **Commit** your changes (`git commit -m 'Add amazing feature'`)
5. **Push** to your branch (`git push origin feature/amazing-feature`)
6. Open a **Pull Request**

Please ensure your code follows the project's coding style and includes appropriate tests and documentation.

## 🗺️ Roadmap

- **Multi-User Support** - Team calendar management
- **Enhanced Voice Recognition** - Improved Urdu language processing
- **Mobile Applications** - Native iOS and Android versions
- **Expanded Language Support** - Additional South Asian languages
- **Advanced Analytics** - Calendar usage insights and suggestions

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

- [Next.js](https://nextjs.org/)
- [OpenAI](https://openai.com/)
- [Pinecone](https://www.pinecone.io/)
- [Google Calendar API](https://developers.google.com/calendar)
- [Tailwind CSS](https://tailwindcss.com/)
- [Radix UI](https://www.radix-ui.com/)

## 👤 Contributors

- [Abdullah Arif](https://github.com/abdullaharif381/) - Project Lead
- [Ibtehaj Ali](https://github.com/Ibtehaj778/)
- [Tahmooras Khan](https://www.linkedin.com/in/tahmooras-khan-8341452a1/)
- [Kabir ud Din Shahab](https://www.linkedin.com/in/kabir-ud-din-shahab-230469262/)

---

<div align="center">
  <p>For support or inquiries, please <a href="https://github.com/abdullaharif381/dora-a3/issues">open an issue</a> on GitHub</p>
  <sub>Built with ❤️ by the DORA team</sub>
</div>
