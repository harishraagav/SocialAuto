# Requirements Document: SocialAuto

## 1. Introduction
SocialAuto is an AI-driven social media automation platform that simplifies the content creation and publishing workflow. Unlike complex developer tools (like n8n) or simple schedulers (like Buffer), SocialAuto combines a **"Canva-like" visual interface** with an **AI-powered workflow generator**. Users can describe their intent in plain English to generate complex posting schedules or manually build them using a drag-and-drop canvas.

## 2. User Stories & Core Features

### 2.1 Unified Account Management ("The Hub")
* **User Story:** As a user, I want to connect my social media accounts (LinkedIn, X, Instagram, Facebook) once so that the system can post on my behalf without constant re-authentication.
* **Acceptance Criteria:**
    * System must support OAuth 2.0 authentication for LinkedIn, X (Twitter), Instagram, and Facebook.
    * Secure storage of access and refresh tokens (encrypted).
    * Dashboard view showing connection status (Active/Expired) for all linked accounts.

### 2.2 Mode A: AI Intent Parser ("Prompt-to-Flow")
* **User Story:** As a user, I want to type "Post a coding tip every Monday at 9 AM to LinkedIn" and have the system build the automation for me.
* **Acceptance Criteria:**
    * Input field for natural language descriptions of the desired workflow.
    * **LLM Integration:** An AI agent must parse the prompt and output a structured JSON configuration representing the workflow nodes and connections.
    * The system must automatically instantiate the correct nodes (e.g., `Schedule Node` -> `AI Text Node` -> `LinkedIn Publish Node`) based on the parsed intent.

### 2.3 Mode B: Visual Workflow Editor ("The Canvas")
* **User Story:** As a user, I want a drag-and-drop interface to tweak the AI-generated workflows or build new ones from scratch, similar to Canva or a simplified n8n.
* **Acceptance Criteria:**
    * **Canvas UI:** A visual editor (using React Flow or similar) allowing users to add, move, and connect nodes.
    * **Node Library:**
        * **Triggers:** Schedule (Cron), Manual Button, Webhook.
        * **Generators:** AI Text (LLM), AI Image (DALL-E/Stable Diffusion).
        * **Modifiers:** Image Resizer, Text Formatter.
        * **Actions:** Post to [Platform].
    * Real-time validation of node connections (e.g., cannot connect an Image output to a Text-only input).

### 2.4 Execution Engine ("The Runner")
* **User Story:** As a user, I want the system to handle the formatting nuances of each platform automatically.
* **Acceptance Criteria:**
    * **"Post Once, Publish Everywhere":** The backend must handle API-specific constraints (e.g., character limits for X, aspect ratios for Instagram) automatically.
    * **Scheduler:** A robust task queue (e.g., BullMQ, Celery) to execute workflows at specific times.
    * **Logs:** Users must see a history of successful and failed executions.

## 3. Non-Functional Requirements
* **Usability:** The UI must prioritize simplicity ("No-Code") over technical flexibility. Visuals should be inviting and clean (Canva-style).
* **Security:** All API tokens must be encrypted at rest (AES-256).
* **Performance:** Workflow generation from AI prompts should take less than 10 seconds.
* **Scalability:** The architecture must support concurrent execution of scheduled tasks for thousands of users.

## 4. Tech Stack Constraints
* **Frontend:** React, React Flow, Tailwind CSS.
* **Backend:** Node.js (or Python FastAPI) for orchestration.
* **Database:**
    * Relational (PostgreSQL) for User Auth & Account data.
    * Document (MongoDB/JSON) for storing Workflow structures.
* **AI:** OpenAI API (or compatible) for intent parsing and content generation.