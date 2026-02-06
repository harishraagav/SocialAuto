<div align="center">

  <h1>SocialAuto 🚀</h1>
  
  <p>
    <strong>AI-Driven Social Media Automation Platform</strong>
  </p>
  
  <p>
    <a href="https://reactjs.org/">
      <img src="https://img.shields.io/badge/Frontend-React%20%2B%20Flow-blue" alt="React">
    </a>
    <a href="https://nodejs.org/">
      <img src="https://img.shields.io/badge/Backend-Node.js-green" alt="Node">
    </a>
    <a href="https://openai.com/">
      <img src="https://img.shields.io/badge/AI-OpenAI%20GPT--4-orange" alt="OpenAI">
    </a>
    <a href="https://opensource.org/licenses/MIT">
      <img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License">
    </a>
  </p>

  <h3>"Post Once, Publish Everywhere."</h3>
  
  <p>
    Combine the ease of Canva with the power of n8n.  
    Describe your workflow in plain English, and watch SocialAuto build it.
  </p>

  <img src="https://via.placeholder.com/800x400.png?text=SocialAuto+Dashboard+Preview" alt="SocialAuto Dashboard" width="100%" />

</div>

<br />

## 📖 Introduction

**SocialAuto** bridges the gap between complex developer tools (like n8n) and simple content schedulers (like Buffer). It automates the content creation and publishing workflow using a unique hybrid approach:

1.  **AI Intent Parser:** Type "Post a coding tip every Monday at 9 AM to LinkedIn," and the system builds the automation for you.
2.  **Visual Canvas:** Tweak generated workflows or build from scratch using a drag-and-drop interface.

Whether you are a solo creator or a marketing agency, SocialAuto handles the API nuances, formatting, and scheduling so you can focus on the content.

---

## ✨ Key Features

### 🧠 Mode A: Prompt-to-Flow
Don't want to drag nodes? Just talk.
- **Natural Language Processing:** Powered by LLMs to parse intent into structured JSON.
- **Auto-Instantiation:** Automatically creates triggers, generators (DALL-E/GPT), and publishing nodes based on your prompt.

### 🎨 Mode B: The Canvas
A "Canva-like" visual editor for granular control.
- **Drag-and-Drop:** Built with React Flow.
- **Node Library:** Includes Triggers (Cron, Webhook), Generators (AI Text/Image), Modifiers (Resizer), and Actions (Social APIs).
- **Real-time Validation:** Prevents invalid connections (e.g., connecting an image output to a text-only input).

### 🌐 The Hub (Unified Auth)
- **One-Click Connect:** OAuth 2.0 integration for LinkedIn, X (Twitter), Instagram, and Facebook.
- **Secure Storage:** Tokens are encrypted at rest using AES-256.
- **Status Monitoring:** Dashboard view of active/expired tokens.

### ⚙️ The Execution Engine
- **Smart Formatting:** Automatically handles platform constraints (aspect ratios, character limits).
- **Robust Scheduling:** Uses BullMQ/Redis for high-concurrency task execution.

---

## 🏗 Architecture

SocialAuto follows a modular monolith architecture with a hybrid data layer.

```mermaid
graph TD
    User[User] --> UI[React Frontend + React Flow]
    UI --> API[Node.js API Gateway]
    
    subgraph "Core Services"
        API --> Auth[Auth Service]
        API --> AI[AI Intent Parser]
        API --> Workflow[Workflow Engine]
        API --> Runner[Execution Runner]
    end
    
    subgraph "Data Layer"
        Auth --> PG[(PostgreSQL)]
        Workflow --> Mongo[(MongoDB)]
        Runner --> Redis[(Redis Queue)]
    end
    
    subgraph "External"
        AI --> OpenAI[OpenAI API]
        Runner --> Socials[LinkedIn / X / FB / Insta]
    end
