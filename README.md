AutoStream Conversational AI Agent (Offline)
Overview

This project implements a fully offline Conversational AI Agent for AutoStream, a fictional SaaS product offering automated video editing tools for content creators.
The agent demonstrates intent-aware, stateful, and action-driven conversational workflows commonly used in production AI systems, while operating entirely without external LLM APIs.

Objectives

Build a conversational agent that goes beyond basic question–answer systems

Demonstrate intent detection, knowledge retrieval, and state management

Implement controlled backend actions based on user intent

Ensure full offline execution for reproducibility and ease of evaluation

Core Capabilities
1. Intent Identification

The agent classifies user input into the following categories:

Casual greetings (e.g., hi, hello)

Product or pricing inquiries

High-intent lead signals (trial, signup, purchase)

Polite conversational messages (sorry, thank you, goodbye)

Unsupported or unclear queries

Intent detection is rule-based and deterministic.

2. Knowledge Retrieval (Local RAG-Style)

The agent retrieves information from a local knowledge base stored in JSON format.

Knowledge includes:

Pricing and features for Basic and Pro plans

Company policies

Support contact information

Responses are generated using a retrieval-first approach based on structured local data.

3. Lead Qualification & Tool Execution

When high-intent behavior is detected, the agent initiates a lead capture workflow:

Collects:

Name

Email

Creator platform (YouTube, Instagram, etc.)

Executes a mock backend function only after all required fields are collected

def mock_lead_capture(name, email, platform):
    print(f"Lead captured successfully: {name}, {email}, {platform}")


Tool execution is strictly gated to prevent premature calls.

4. Stateful Conversation Management

Conversation context is maintained across multiple turns

Lead capture progress is tracked step-by-step

Ensures consistent and logical dialogue flow

State is managed using in-memory session storage.

5. Support Assistant Fallback

For unsupported or ambiguous queries, the agent:

Responds politely and safely

Provides official support contact details

Avoids speculative or incorrect responses

Project Structure
autostream-chatbot/
│
├── autostream_kb.json      
├── chatbot.ipynb           
├── requirements.txt        
└── README.md               

Technology Stack

Language: Python 3.9+

Execution Environment: Jupyter Notebook

State Management: In-memory session dictionary

Data Storage: JSON

Design Approach: Rule-based agentic workflow

How to Run Locally
1. Clone the Repository
git clone https://github.com/your-username/autostream-chatbot.git
cd autostream-chatbot

2. Install Dependencies
pip install -r requirements.txt

3. Run the Notebook
jupyter notebook chatbot.ipynb


Execute each cell sequentially to start the chatbot.

Sample Conversation Flow
User: Hi
Agent: Hello! I’m your AutoStream assistant. How can I help you today?

User: Tell me about pricing
Agent: Retrieves pricing from the local knowledge base

User: I want to try the Pro plan for my YouTube channel
Agent: Detects high intent and begins lead capture

User: My name is Alex
User: alex@email.com
User: YouTube
Agent: Lead captured successfully

WhatsApp Integration (Conceptual)

To integrate this agent with WhatsApp:

Use WhatsApp Business API or Twilio WhatsApp API

Receive incoming messages via webhooks

Forward messages to the chatbot logic

Return agent responses through the API

Persist conversation state using:

Redis

Database

Session cache

This enables real-time WhatsApp conversations while preserving dialogue context.

Future Enhancements

Integration with production LLMs

Vector-based semantic retrieval

Web interface using Streamlit or Flask

Persistent database-backed memory

Lead analytics and monitoring dashboard
