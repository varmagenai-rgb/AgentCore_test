A hands-on crash course for building AI agents with Amazon Bedrock AgentCore, LangGraph, and LangChain. This project demonstrates how to wire together an agent runtime, memory/checkpointing on AWS, vector search with FAISS, and multiple LLM providers (AWS Bedrock and Groq).

Overview
This repository contains example scripts and notebooks that walk through:

Building agents with LangGraph

Deploying agents to Amazon Bedrock AgentCore

Persisting agent state with LangGraph checkpointing on AWS

Local vector search using FAISS

Embeddings via HuggingFace / sentence-transformers

Calling models through LangChain AWS (Bedrock) and Groq

Tech Stack
Component	Purpose
bedrock-agentcore	Agent runtime for Amazon Bedrock AgentCore
bedrock-agentcore-starter-toolkit	Tooling to scaffold and deploy agents
langgraph	Agent orchestration and state graphs
langgraph-checkpoint-aws	Persistent checkpointing on AWS
langchain[aws]	LangChain integrations for AWS Bedrock
langchain-community, langchain-groq, langchain-huggingface	Community and provider integrations
faiss-cpu	Local vector similarity search
sentence-transformers	Local embedding models
Prerequisites
Python 3.13+

uv — fast Python package and environment manager

AWS account with access to Amazon Bedrock and AgentCore

Groq API key (optional, only if you use the Groq examples)

Install uv (Windows PowerShell)
powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
Setup
1. Clone the repository
powershell
git clone https://github.com/<your-username>/agentcore-crash-course.git
cd agentcore-crash-course
2. Install dependencies
uv creates and manages the .venv automatically:

powershell
uv sync
3. Configure environment variables
Copy the example file and fill in your own values:

powershell
Copy-Item .env.example .env
Then edit .env:

dotenv
# AWS credentials for Bedrock / AgentCore
AWS_ACCESS_KEY_ID=your_access_key_id
AWS_SECRET_ACCESS_KEY=your_secret_access_key
AWS_REGION=us-east-1

# Groq (optional)
GROQ_API_KEY=your_groq_api_key
Never commit .env. It is already listed in .gitignore.

4. Run an example
Always run scripts through uv run so the project's virtual environment is used:

powershell
uv run python 00_langgraph_agent.py
Or activate the environment manually:

powershell
.\.venv\Scripts\activate
python 00_langgraph_agent.py
Project Structure
text
.
├── 00_langgraph_agent.py      # Entry-point example: LangGraph agent
├── pyproject.toml             # Project metadata and dependencies
├── .env.example               # Template for environment variables (no secrets)
├── .gitignore                 # Excludes .env, .venv, and caches
└── README.md
Adjust the file list above to match the scripts actually present in your repository.

Security: Handling Keys
This project follows a strict no-secrets-in-git policy:

.env is ignored via .gitignore and must never be committed.

Only .env.example (with placeholder values) is tracked.

If a key is ever exposed in Git history, revoke and rotate it immediately on the issuing platform (AWS IAM, Groq console, etc.), then clean the history with git filter-repo or rebuild the repository.

Troubleshooting
faiss-cpu fails to install on Windows

faiss-cpu only ships Windows wheels for specific Python versions. This project pins a version compatible with Python 3.13. If you change the Python version, verify a matching wheel exists on PyPI before running uv sync.

ModuleNotFoundError when running a script

You are probably using the system python instead of the project environment. Run the script with uv run python <script>.py, or activate .venv first.