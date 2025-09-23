# Learning Kit for TradingAgents

This document is your guide to understanding the TradingAgents project, from a high-level overview to the details of the code.

## 1. Project Overview

**TradingAgents** is a multi-agent financial trading framework that uses Large Language Models (LLMs) to analyze market data and make trading decisions. It simulates a trading firm with specialized agents for different types of analysis.

The core of the project is built with **LangGraph**, a library for building stateful, multi-agent applications with LLMs.

## 2. Core Concepts

*   **Multi-Agent System:** The project uses a team of AI agents that collaborate to analyze financial data. Each agent has a specific role.
*   **LangGraph:** This is the key library used to define and run the multi-agent system. It manages the state and the flow of information between agents.
*   **Agent Roles:**
    *   **Fundamental Analyst:** Evaluates company financials.
    *   **Sentiment Analyst:** Gauges market mood from news and social media.
    *   **Technical Analyst:** Uses technical indicators to find trading patterns.
    *   **Trader:** Makes trading decisions based on the analysis of other agents.
    *   **Risk Manager:** Evaluates and mitigates risks in trading strategies.

## 3. Project Structure

Here are the most important files and directories:

*   `main.py`: A script to run the `TradingAgentsGraph` with a pre-defined configuration.
*   `cli/main.py`: The entry point for the interactive command-line interface (CLI).
*   `requirements.txt`: A list of all the Python libraries needed for the project.
*   `tradingagents/default_config.py`: A centralized configuration file for managing settings like LLMs and data sources.
*   **`tradingagents/`**: The core directory of the project.
    *   **`agents/`**: Contains the implementation of all the different agents. This is a great place to start exploring the logic of the system.
    *   **`dataflows/`**: Manages data from various sources like Finnhub, Yahoo Finance, and Reddit.
    *   **`graph/`**: Defines the structure of the multi-agent system using LangGraph, including how the agents interact and share information.

## 4. How to Run the Project

### Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/TauricResearch/TradingAgents.git
    cd TradingAgents
    ```

2.  **Create a virtual environment:**
    ```bash
    conda create -n tradingagents python=3.13
    conda activate tradingagents
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

### Required APIs

You will need API keys from Finnhub and OpenAI.

```bash
export FINNHUB_API_KEY=$YOUR_FINNHUB_API_KEY
export OPENAI_API_KEY=$YOUR_OPENAI_API_KEY
```

### Running the Application

You can run the project in two ways:

*   **Command-Line Interface (CLI):**
    ```bash
    python -m cli.main
    ```
    This will launch an interactive CLI that allows you to select the ticker, date, and other parameters.

*   **Python Script:**
    ```bash
    python main.py
    ```
    This will run the `TradingAgentsGraph` with a pre-defined configuration from `tradingagents/default_config.py`.

## 5. A 5-Day Learning Plan

Here is a suggested plan to help you learn the codebase.

### Day 1: High-Level Map

*   **Goal:** Understand the project's purpose and how to run it.
*   **Tasks:**
    1.  Read this `LearningKit.md` file.
    2.  Follow the steps in the "How to Run the Project" section to get the application running.
    3.  Run both the CLI and the `main.py` script to see how they work.
*   **Quiz:**
    *   What is the main purpose of the TradingAgents project?
    *   What is LangGraph used for in this project?
    *   What are the two ways to run the application?

### Day 2: Explore the Agents

*   **Goal:** Understand the roles and responsibilities of the different agents.
*   **Tasks:**
    1.  Explore the `tradingagents/agents/` directory.
    2.  Read the code for the `FundamentalsAnalyst` (`tradingagents/agents/analysts/fundamentals_analyst.py`) to see how it analyzes financial data.
    3.  Read the code for the `Trader` (`tradingagents/agents/trader/trader.py`) to see how it makes decisions.
*   **Quiz:**
    *   What kind of data does the `NewsAnalyst` process?
    *   Which agent is responsible for making the final trading decision?
    *   Where would you look to understand how the agents collaborate?

### Day 3: Understand the Data Flow

*   **Goal:** Learn how the project gets data from external sources.
*   **Tasks:**
    1.  Explore the `tradingagents/dataflows/` directory.
    2.  Look at `finnhub_utils.py` and `yfin_utils.py` to see how the project interacts with financial data APIs.
    3.  Read `googlenews_utils.py` and `reddit_utils.py` to understand how news and social media data are collected.
*   **Quiz:**
    *   What are the main data sources for this project?
    *   If you wanted to add a new data source, which directory would you modify?
    *   What kind of information does `finnhub_utils.py` provide?

### Day 4: Trace the Graph

*   **Goal:** Understand how the agents are connected and how information flows between them.
*   **Tasks:**
    1.  Explore the `tradingagents/graph/` directory.
    2.  Read `trading_graph.py` to see how the LangGraph is constructed.
    3.  Look at `conditional_logic.py` to understand how the graph makes decisions about which agent to run next.
*   **Quiz:**
    *   What is the role of the `AgentState` in `tradingagents/agents/utils/agent_states.py`?
    *   How does the graph pass information from one agent to another?
    *   Which file defines the edges and nodes of the LangGraph?

### Day 5: Ship a Tiny Change

*   **Goal:** Make a small change to the code to solidify your understanding.
*   **Tasks:**
    1.  **Idea:** Modify the prompt for one of the agents. For example, you could change the prompt for the `NewsAnalyst` in `tradingagents/agents/analysts/news_analyst.py` to focus on a specific aspect of the news.
    2.  Run the application and see how your change affects the output.
*   **Quiz:**
    *   What was the effect of your change?
    *   What other small changes could you make to experiment with the system?
    *   What part of the codebase do you want to explore next?