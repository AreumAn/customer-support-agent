# Customer Support Agent

A multi-agent customer support system built with the OpenAI Agents framework. It provides a Streamlit-based web interface that automatically classifies customer inquiries and routes them to the appropriate specialist agent.

## Features

### 🤖 Multi-Agent System

- **Triage Agent**: Analyzes customer inquiries and routes them to the appropriate specialist agent
- **Technical Support Agent**: Provides product technical support and troubleshooting
- **Billing Support Agent**: Handles payment, refund, and subscription inquiries
- **Order Management Agent**: Manages order status, shipping, and returns
- **Account Management Agent**: Handles account access, security, and profile management

### 🛡️ Guardrails

- **Input Guardrails**: Filters out topics unrelated to customer support
- **Output Guardrails**: Prevents agents from providing information outside their area of expertise

### 💬 Real-time Streaming Chat

- Streamlit-based interactive interface
- Real-time response streaming
- Conversation history management (SQLite)

### 🔧 Specialized Tool Sets

Each agent uses specialized tools:

**Technical Support:**
- Run diagnostic checks
- Provide troubleshooting steps
- Escalate to engineering team

**Billing Support:**
- Look up billing history
- Process refund requests
- Update payment methods
- Apply account credits

**Order Management:**
- Look up order status
- Initiate return process
- Schedule redelivery
- Expedite shipping

**Account Management:**
- Reset user passwords
- Enable two-factor authentication
- Update account email addresses
- Deactivate accounts
- Export account data

## Project Structure

```
customer-support-agent/
├── main.py                    # Streamlit main application
├── models.py                  # Pydantic model definitions
├── tools.py                   # Agent tool functions
├── output_guardrails.py      # Output guardrail definitions
├── my_agents/
│   ├── triage_agent.py       # Triage agent
│   ├── technical_agent.py   # Technical support agent
│   ├── billing_agent.py      # Billing support agent
│   ├── order_agent.py        # Order management agent
│   └── account_agent.py      # Account management agent
├── customer-support-memory.db # SQLite session database
└── pyproject.toml            # Project dependencies
```

## Installation & Setup

### Requirements

- Python 3.13 or higher
- OpenAI API key

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd customer-support-agent
```

2. Install dependencies:
```bash
# Using uv
uv sync

# Or using pip
pip install -r requirements.txt
```

3. Set up environment variables:
Create a `.env` file and add your OpenAI API key:
```
OPENAI_API_KEY=your_api_key_here
```

### Running

```bash
streamlit run main.py
```

Access the application at `http://localhost:8501` in your browser.

## Usage

1. **Start Chatting**: Enter customer inquiries in the message input field.
2. **Auto-Routing**: The Triage Agent analyzes inquiries and automatically transfers to the appropriate specialist agent.
3. **Specialist Support**: Each specialist agent uses domain-specific tools to resolve issues.
4. **Conversation History**: All conversations are saved to a SQLite database and persist across sessions.

### Sidebar Features

- **Reset Memory**: Clear conversation history
- **Tool Usage Logs**: View tools used by each agent
- **Agent Transfer Logs**: Track handoffs between agents

## Customer Tier Support

The system provides different levels of service based on customer tiers (basic, premium, enterprise):

- **Premium/Enterprise Customers**: Priority processing, faster response times, additional benefits
- **Basic Customers**: Standard support process

## How Guardrails Work

### Input Guardrails
Validates that customer input is related to customer support topics. Displays "I can't help you with that." message for off-topic requests.

### Output Guardrails
Prevents agents from providing information outside their expertise. For example, if a Technical Support Agent generates a response containing billing or order information, it will be blocked.

## Tech Stack

- **OpenAI Agents**: Multi-agent framework
- **Streamlit**: Web interface
- **SQLite**: Session and conversation history storage
- **Pydantic**: Data model validation
- **Python 3.13+**: Programming language

## Dependencies

Main dependencies are defined in `pyproject.toml`:

- `openai-agents[voice]>=0.2.8`
- `streamlit>=1.48.1`
- `python-dotenv>=1.1.1`
- `numpy>=2.3.2`
- `sounddevice>=0.5.2`

## Development

### Adding Agents

To add a new specialist agent:

1. Create a new agent file in the `my_agents/` directory
2. Add necessary tool functions to `tools.py`
3. Add the new agent to the `handoffs` list in `triage_agent.py`

### Adding Tools

To add a new tool, define a function in `tools.py` using the `@function_tool` decorator.

## License

This project is created for educational purposes.

## Contributing

Issues and pull requests are welcome. If you have suggestions for improving the project, please create an issue.
