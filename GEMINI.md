# Gemini Code Assistant Report

## Project Overview

This project, **TradingAgents**, is a multi-agent financial trading framework that leverages Large Language Models (LLMs) to analyze market data and make trading decisions. The framework is designed to simulate the structure of a real-world trading firm, with different agents specializing in various aspects of financial analysis.

The core of the project is built using **LangGraph**, a library for building stateful, multi-agent applications with LLMs. The framework is highly modular, with different agents responsible for tasks such as:

*   **Fundamental Analysis:** Evaluating company financials and performance metrics.
*   **Sentiment Analysis:** Gauging market mood by analyzing social media and news.
*   **Technical Analysis:** Using technical indicators to identify trading patterns.
*   **Trading:** Making informed trading decisions based on the analysis of other agents.
*   **Risk Management:** Evaluating and adjusting trading strategies to mitigate risk.

The project uses a variety of data sources, including Finnhub, Yahoo Finance, and Reddit, to gather financial data and news. It also uses a variety of LLMs, including models from OpenAI, Anthropic, and Google, to power the different agents.

## Building and Running

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

*   **Finnhub API:**
    ```bash
    export FINNHUB_API_KEY=$YOUR_FINNHUB_API_KEY
    ```

*   **OpenAI API:**
    ```bash
    export OPENAI_API_KEY=$YOUR_OPENAI_API_KEY
    ```

### Running the Application

*   **Command-Line Interface (CLI):**
    ```bash
    python -m cli.main
    ```
    This will launch an interactive CLI that allows you to select the ticker, date, analysts, and other parameters for the analysis.

*   **Python Script:**
    ```bash
    python main.py
    ```
    This will run the `TradingAgentsGraph` with a pre-defined configuration.

## Development Conventions

*   **Configuration:** The project uses a centralized configuration file, `tradingagents/default_config.py`, to manage all the settings for the application. This makes it easy to switch between different LLMs, data sources, and other parameters.
*   **Modularity:** The project is highly modular, with different agents and components organized into separate files and directories. This makes it easy to understand, maintain, and extend the codebase.
*   **State Management:** The project uses LangGraph to manage the state of the application. The state is passed between the different agents in the graph, allowing them to share information and collaborate on the analysis.
*   **Error Handling:** The project includes error handling to gracefully handle situations where data is not available or an API call fails.
*   **Debugging:** The project includes a debug mode that can be enabled to print out detailed information about the execution of the graph. This is useful for debugging and understanding how the different agents are interacting.
