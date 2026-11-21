# TripMate – AI-Powered Travel Planning Assistant

An intelligent multi-agent travel planning system built using **LangGraph and the Model Context Protocol (MCP)**. TripMate uses a Supervisor-based architecture to coordinate specialized agents, validate user requests through input guardrails, and generate travel plans with Human-in-the-Loop (HITL) approval.

The system demonstrates how multiple AI agents can collaborate to handle complex travel-planning workflows while maintaining control, reliability, and human oversight.

## Key Features

- **Multi-Agent Architecture:** Coordinates multiple specialized agents using LangGraph.
- **Supervisor Agent:** Manages agent communication, delegates tasks, and coordinates the overall workflow.
- **Input Guardrails:** Validates incoming user requests before processing them.
- **Human-in-the-Loop (HITL):** Allows users to review, approve, or request modifications to generated travel plans.
- **MCP Integration:** Uses the Model Context Protocol to connect AI agents with external tools and services.
- **Weather Integration:** Demonstrates external tool integration through a custom MCP weather server.
- **Interactive Web Interface:** Provides a user-friendly interface for submitting travel requests and reviewing generated plans.
- **API-Based Architecture:** Exposes endpoints for travel planning, approval, and health monitoring.

## Tech Stack

| Category | Technologies |
|---|---|
| Programming Language | Python |
| Agent Orchestration | LangGraph |
| AI Framework | LangChain |
| Tool Integration | Model Context Protocol (MCP) |
| Backend | FastAPI |
| Frontend | HTML, CSS, JavaScript |
| API Communication | REST APIs |
| Environment Management | Python Virtual Environment |

## System Architecture

TripMate follows a Supervisor-based multi-agent architecture.

1. **User Request:** The user submits a travel-planning request through the web interface.
2. **Input Guardrails:** The request is validated to ensure it meets the system's requirements.
3. **Supervisor Agent:** The Supervisor analyzes the request and coordinates the necessary agents.
4. **Agent Execution:** Specialized agents perform their assigned tasks using available tools and MCP integrations.
5. **Plan Generation:** The system generates a structured travel plan based on the collected information.
6. **Human Review:** The generated plan is presented to the user for approval.
7. **Approval or Revision:** The user can approve the plan or provide feedback for modifications.

## Project Structure

```text
TripMate/
│
├── app.py
├── backend.py
├── mcp_client.py
├── custom_weather_mcp_server.py
│
├── templates/
│   └── index.html
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── requirements.txt
├── .env.example
├── .gitignore
└── README.md
```

### Core Components

| File / Directory | Description |
|---|---|
| `app.py` | FastAPI application providing the web interface and API endpoints. |
| `backend.py` | Implements the core travel-planning logic and LangGraph agent orchestration. |
| `mcp_client.py` | Contains client-side helpers for communicating with MCP servers. |
| `custom_weather_mcp_server.py` | Example MCP server providing weather-related tools. |
| `templates/` | Contains HTML templates for the web interface. |
| `static/` | Contains frontend assets, including CSS, JavaScript, and images. |
| `requirements.txt` | Lists the Python dependencies required by the project. |
| `.env.example` | Provides a template for environment configuration. |

## Getting Started

Follow these instructions to set up and run TripMate locally.

### Prerequisites

Make sure you have the following installed:

- Python 3.10 or higher
- Git
- pip
- An API key for the LLM provider configured by the application

### 1. Clone the Repository

```bash
git clone https://github.com/anushka-tiwari07/TripMate.git
cd TripMate
```

### 2. Create a Virtual Environment

```bash
python -m venv .venv
```

### 3. Activate the Virtual Environment

For Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

For macOS/Linux:

```bash
source .venv/bin/activate
```

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

### 5. Configure Environment Variables

Create a `.env` file in the root directory and add the API keys required by your configured LLM provider and integrations.

Example:

```env
OPENAI_API_KEY=your_api_key_here
```

Add other environment variables required by your MCP servers or integrations.

**Note:** Never commit your `.env` file or expose API keys in the repository.

### 6. Run the Application

Start the FastAPI application:

```bash
uvicorn app:app --reload --host 127.0.0.1 --port 8000
```

Alternatively, if supported by the application:

```bash
python app.py
```

### 7. Access TripMate

Open your browser and navigate to:

```text
http://127.0.0.1:8000
```

You can now submit travel-planning requests and interact with the TripMate interface.

## Running the MCP Weather Server

TripMate includes an example custom MCP server for weather-related tool integration.

To run it independently, open another terminal, activate the virtual environment, and execute:

```bash
python custom_weather_mcp_server.py
```

The MCP client can use this server to demonstrate communication with external tools and services.

## API Documentation

TripMate exposes the following API endpoints:

### 1. Create or Resume a Travel Plan

**Endpoint:** `POST /api/travel`

Accepts a travel-planning request and creates or resumes a planning thread.

Request Body:

```json
{
    "message": "Plan a 5-day trip to Manali",
    "thread_id": "optional-thread-id"
}
```

### 2. Approve or Request Revisions

**Endpoint:** `POST /api/travel/approve`

Allows users to approve a generated travel plan or request changes.

Request Body:

```json
{
    "thread_id": "thread-id",
    "approved": true,
    "feedback": "Looks good!"
}
```

Set `approved` to `false` when requesting revisions and provide feedback describing the required changes.

### 3. Health Check

**Endpoint:** `GET /health`

Returns the application's health status and supported features.

## Human-in-the-Loop Workflow

TripMate incorporates Human-in-the-Loop approval to ensure that generated travel plans can be reviewed before proceeding.

The workflow supports:

- Draft generation through the multi-agent system.
- Presentation of generated plans for user review.
- Explicit approval from the user.
- Feedback-based revision requests.
- Resumption of the planning workflow using the associated thread ID.

This approach keeps the user involved in important decisions instead of relying entirely on autonomous agent execution.

## Future Enhancements

Potential areas
